---
title: Resync, méthode-exemple (VC ++) | Documents Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Resync method [ADO], VC++ example
ms.assetid: d34dfd26-9ca7-4c9c-a918-396f05fecca9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a84755816e923fb615a06aad62a466155922b0cf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="resync-method-example-vc"></a>Resync, méthode-exemple (VC ++)
Cet exemple montre comment utiliser le [Resync](../../../ado/reference/ado-api/resync-method.md) méthode pour actualiser les données dans un jeu d’enregistrements statique.  
  
```  
// Resync_Method_Sample.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void ResyncX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   ResyncX();  
   ::CoUninitialize();  
}  
  
void ResyncX() {  
   // Define string variables.  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB:: namespace.  
   _RecordsetPtr pRstTitles = NULL;  
  
   try {  
      // Open recordset for titles table.  
      TESTHR(pRstTitles.CreateInstance(__uuidof(Recordset)));  
      pRstTitles->CursorLocation = adUseClient;  
      pRstTitles->CursorType = adOpenStatic;  
      pRstTitles->LockType = adLockBatchOptimistic;  
      pRstTitles->Open ("titles", strCnn, adOpenStatic, adLockBatchOptimistic, adCmdTable);  
  
      // Change the type of the first title in the recordset.  
      pRstTitles->Fields->GetItem("type")->Value = (_bstr_t) ("database");  
  
      // Display the results of the change.  
      printf("\nBefore resync: \n\n");  
  
      printf("Title - %s\n\n",   
         (LPSTR)(_bstr_t) pRstTitles->Fields->GetItem("title")->Value);  
  
      printf("Type - %s\n\n",  
         (LPSTR)(_bstr_t) pRstTitles->Fields->GetItem("type")->Value);  
  
      // Resync with database.  
      pRstTitles->Resync(adAffectAll,adResyncAllValues);  
  
      // Display the results of the resynch.  
      printf("\n\nAfter resync: \n\n");  
  
      printf("Title - %s\n\n",  
         (LPSTR)(_bstr_t) pRstTitles->Fields->GetItem("title")->Value);  
  
      printf("Type - %s\n\n",  
         (LPSTR)(_bstr_t) pRstTitles->Fields->GetItem("type")->Value);  
   }  
   catch (_com_error &e) {  
      // Display errors, if any. Pass a connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstTitles->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
      case VT_BSTR:  
         PrintComError(e);  
         break;  
      case VT_DISPATCH:  
         PrintProviderError(vtConnect);  
         break;  
      default:  
         printf("Errors occured.");  
         break;  
      }  
   }  
  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen) {  
         pRstTitles->CancelBatch(adAffectAll);  
         pRstTitles->Close();  
      }  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0 ) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s\n", pErr->Number, (LPCSTR) pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print COM errors.   
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Resync, méthode](../../../ado/reference/ado-api/resync-method.md)