---
title: IBCPSession2::BCPSetBulkMode |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BCPSetBulkMode function
ms.assetid: babba19f-e67b-450c-b0e6-523a0f9d23ab
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f0c0ec3e7f76da7eb908cf2154cd33a2ee55b40
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427517"
---
# <a name="ibcpsession2bcpsetbulkmode"></a>IBCPSession2::BCPSetBulkMode
  IBCPSession2::BCPSetBulkMode 提供替代[ibcpsession:: Bcpcolfmt &#40;OLE DB&#41; ](ibcpsession-bcpcolfmt-ole-db.md)來指定資料行格式。 與不同的是，它可以設定個別的資料行格式屬性，ibcpsession:: Bcpcolfmt IBCPSession2::BCPSetBulkMode 設定所有屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPSetBulkMode (  
      int property,  
   void * pField,  
   int cbField,  
   void * pRow,  
   int cbRow  
);  
```  
  
## <a name="arguments"></a>引數  
 *property*  
 類型為 BYTE 的常數。 如需常數的清單，請參閱＜備註＞一節中的表格。  
  
 *pField*  
 欄位結束字元值的指標。  
  
 cbField  
 欄位結束字元值的長度 (以位元組為單位)。  
  
 pRow  
 資料列結束字元值的指標。  
  
 cbRow  
 資料列結束字元值的長度 (以位元組為單位)。  
  
## <a name="returns"></a>傳回值  
 IBCPSession2::BCPSetBulkMode 會傳回下列其中一項：  
  
|||  
|-|-|  
|`S_OK`|此方法已成功。|  
|`E_FAIL`|如需詳細的資訊，請使用 ISQLServerErrorInfo 介面發生提供者特有的錯誤。|  
|`E_UNEXPECTED`|此方法的呼叫是非預期的。 比方說，`IBCPSession2::BCPInit`方法不會呼叫 IBCPSession2::BCPSetBulkMode 之前呼叫。|  
|`E_INVALIDARG`|此引數無效。|  
|`E_OUTOFMEMORY`|記憶體不足的錯誤。|  
  
## <a name="remarks"></a>備註  
 IBCPSession2::BCPSetBulkMode 可用來大量複製查詢或資料表。 IBCPSession2::BCPSetBulkMode 來大量複製查詢陳述式，它必須先呼叫才能呼叫`IBCPSession::BCPControl(BCP_OPTIONS_HINTS, …)`來指定查詢陳述式。  
  
 您應該避免在單一命令文字中結合 RPC 呼叫語法與批次查詢語法 (例如 `{rpc func};SELECT * from Tbl`)。  這會導致 icommandprepare:: Prepare 傳回錯誤，並讓您無法擷取中繼資料。 如果您需要在單一命令文字中結合預存程序執行與批次查詢，請使用 ODBC CALL 語法 (例如 `{call func}; SELECT * from Tbl`)。  
  
 下表列出的常數*屬性*參數。  
  
|屬性|描述|  
|--------------|-----------------|  
|BCP_OUT_CHARACTER_MODE|指定字元輸出模式。<br /><br /> 對應至在 BCP 中的 – c 選項。EXE，並具有的 ibcpsession:: Bcpcolfmt *eUserDataType*屬性設定為`BCP_TYPE_SQLCHARACTER`。|  
|BCP_OUT_WIDE_CHARACTER_MODE|指定 Unicode 輸出模式。<br /><br /> 對應至在 BCP 中的 – w 選項。EXE 和使用的 ibcpsession:: Bcpcolfmt *eUserDataType*屬性設定為`BCP_TYPE_SQLNCHAR`。|  
|BCP_OUT_NATIVE_TEXT_MODE|指定非字元類型的原生類型和字元類型的 Unicode。<br /><br /> 對應到 BCP 中的 – N 選項。EXE 和使用的 ibcpsession:: Bcpcolfmt *eUserDataType*屬性設定為`BCP_TYPE_SQLNCHAR`如果資料行類型是字串或`BCP_TYPE_DEFAULT`如果不是字串。|  
|BCP_OUT_NATIVE_MODE|指定原生資料庫類型。<br /><br /> 對應到 BCP 中的 – n 選項。EXE 和使用的 ibcpsession:: Bcpcolfmt *eUserDataType*屬性設定為`BCP_TYPE_DEFAULT`。|  
  
 您可以呼叫 ibcpsession:: Bcpcontrol 和 IBCPSession2::BCPSetBulkMode IBCPSession2::BCPSetBulkMode 不衝突的 ibcpsession:: Bcpcontrol 選項。 例如，您可以在其中呼叫 ibcpsession:: Bcpcontrol 與`BCP_OPTION_FIRST`和 IBCPSession2::BCPSetBulkMode。  
  
 您不能呼叫 ibcpsession:: Bcpcontrol 與`BCP_OPTION_TEXTFILE`和 IBCPSession2::BCPSetBulkMode。  
  
 如果您嘗試呼叫的函式呼叫的順序，其中包含 ibcpsession:: Bcpcolfmt、 ibcpsession:: Bcpcontrol，以及 ibcpsession:: Bcpreadfmt IBCPSession2::BCPSetBulkMode，其中一個函式呼叫會傳回順序錯誤失敗。 如果您選擇要更正失敗，請呼叫 ibcpsession:: Bcpinit 來重設設定並重新開始。  
  
 下表將呈現產生函數順序錯誤之函數呼叫的部分範例。  
  
 呼叫順序  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_IN);  
BCPSetBulkMode();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPSetBulkMode();  
BCPReadFmt();  
```  
  
```  
BCPInit(NULL, "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_HINTS, "select …");  
BCPSetBulkMode();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPSetBulkMode();  
BCPColFmt();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPReadFmt();  
BCPColFmt();  
```  
  
```  
BCPInit(NULL, "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPSetBulkMode();  
BCPControl(BCP_OPTION_HINTS, "select …");  
BCPReadFmt();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPColumns();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPSetColFmt();  
```  
  
## <a name="example"></a>範例  
 下列範例會使用不同的 IBCPSession2::BCPSetBulkMode 設定來建立四個檔案。  
  
```  
  
// compile with: sqlncli11.lib oleaut32.lib ole32.lib  
  
#include <stdio.h>  
#include "sqlncli.h"  
  
IDBInitialize*  g_pIDBInitialize = NULL;  
IBCPSession2 * g_pIBcpSession = NULL;  
class COLEDBPropSet : public DBPROPSET {  
public:  
   COLEDBPropSet() {  
      rgProperties = NULL;  
      cProperties = 0;  
   };  
   COLEDBPropSet(const GUID& guid) {  
      rgProperties = NULL;  
      cProperties = 0;  
      guidPropertySet = guid;  
   };  
   ~COLEDBPropSet() {  
      for ( ULONG i = 0 ; i < cProperties ; i++ )  
         VariantClear(&rgProperties[i].vValue);  
      CoTaskMemFree(rgProperties);  
   }  
   void SetGUID(const GUID& guid) {  
      guidPropertySet = guid;  
   };  
   bool AddProperty(DWORD dwPropertyID, bool bValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID = dwPropertyID;  
      rgProperties[cProperties].vValue.vt = VT_BOOL;  
      rgProperties[cProperties].vValue.boolVal = (bValue) ? VARIANT_TRUE : VARIANT_FALSE;  
      cProperties++;  
      return true;  
   };  
   bool AddProperty(DWORD dwPropertyID, long nValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID  = dwPropertyID;  
      rgProperties[cProperties].vValue.vt     = VT_I4;  
      rgProperties[cProperties].vValue.lVal   = nValue;  
      cProperties++;  
      return true;  
   };  
   bool AddProperty(DWORD dwPropertyID,LPCWSTR szValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID = dwPropertyID;  
      rgProperties[cProperties].vValue.vt = VT_BSTR;  
      rgProperties[cProperties].vValue.bstrVal = SysAllocString(szValue);  
      cProperties++;  
      return true;  
   };  
   bool Add() {  
      DBPROP* p = (DBPROP*)CoTaskMemRealloc(rgProperties, (cProperties + 1) * sizeof(DBPROP));  
      if (p != NULL) {  
         rgProperties = p;  
         rgProperties[cProperties].dwOptions = DBPROPOPTIONS_REQUIRED;  
         rgProperties[cProperties].colid = DB_NULLID;  
         rgProperties[cProperties].vValue.vt = VT_EMPTY;  
         return true;  
      }  
      else  
         return false;  
   };  
};  
  
void OLEDBCleanUp() {  
   if (g_pIDBInitialize) {  
      g_pIDBInitialize->Release();  
      g_pIDBInitialize = NULL;  
   }  
   if (g_pIBcpSession) {  
      g_pIBcpSession->Release();  
      g_pIBcpSession = NULL;  
   }  
}  
  
BOOL MakeOLEDBConnect(LPWSTR  pServer) {  
   BOOL ret = true;  
   IDBProperties * pIDBProperties = NULL;  
   IDBCreateSession * pIDBCreateSession = NULL;  
   COLEDBPropSet PropSet(DBPROPSET_DBINIT);  
   COLEDBPropSet BcpProperty(DBPROPSET_SQLSERVERDATASOURCE);  
   try {  
      HRESULT hr = CoInitializeEx(NULL,COINIT_MULTITHREADED);   
      hr = CoCreateInstance(SQLNCLI_CLSID, NULL, CLSCTX_INPROC_SERVER, IID_IDBInitialize, (LPVOID *)&g_pIDBInitialize);  
      if (FAILED(hr)) {  
         printf("CoCreateInstance failed\n");  
         return false;  
      }  
      PropSet.AddProperty(DBPROP_INIT_DATASOURCE, (LPWSTR)pServer);  
      PropSet.AddProperty(DBPROP_AUTH_INTEGRATED, L"SSPI");  
      hr = g_pIDBInitialize->QueryInterface(IID_IDBProperties, (void**) &pIDBProperties);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->QueryInterface(IID_IDBProperties...) failed\n");  
         throw false;  
      }  
      hr = pIDBProperties->SetProperties(1, &PropSet);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->SetProperties(...) failed\n");  
         throw false;  
      }  
      hr = g_pIDBInitialize->Initialize();  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->Initialize() failed\n");  
         throw false;  
      }  
      BcpProperty.AddProperty(SSPROP_ENABLEFASTLOAD, true);  
      BcpProperty.AddProperty(SSPROP_ENABLEBULKCOPY, true);  
      hr = pIDBProperties->SetProperties(1, &BcpProperty);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->SetProperties() for bcp failed\n");  
         throw false;  
      }  
      hr = g_pIDBInitialize->QueryInterface(IID_IDBCreateSession, (void**) &pIDBCreateSession);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->QueryInterface(IID_IDBCreateSession..) failed\n");  
         throw false;  
      }  
  
      hr = pIDBCreateSession->CreateSession(NULL, IID_IBCPSession2, (IUnknown**) &g_pIBcpSession);  
      if (FAILED(hr)) {  
         printf("g_pIDBCreateSession->CreateSession() failed\n");  
         throw false;  
      }  
   }  
   catch(...) {  
      ret = false;  
   }  
   if (pIDBProperties)  
      pIDBProperties->Release();  
   if (pIDBCreateSession)  
      pIDBCreateSession->Release();  
   return ret;  
}  
  
BOOL BCPSetBulkMode(LPWSTR pszServer, LPTSTR pszQureryOut, char BCPType, LPWSTR pszDataFile) {  
   HRESULThr;  
   if (!MakeOLEDBConnect(pszServer))  
      return false;  
   hr = g_pIBcpSession->BCPInit(NULL, pszDataFile, NULL, BCP_DIRECTION_OUT );   // bcp init for queryout  
   if (FAILED(hr)) {  
      printf("BCP init failed\n");  
      OLEDBCleanUp();  
      return false;  
   }  
   // setbulkmode  
   char ColTerm[] = "\t";  
   char RowTerm[] = "\r\n";  
   wchar_t wColTerm[] = L"\t";  
   wchar_t wRowTerm[] = L"\r\n";  
   BYTE * pColTerm = NULL;  
   int cbColTerm = NULL;  
   BYTE * pRowTerm = 0;  
   int cbRowTerm = 0;  
   int bulkmode = -1;  
  
   if(BCPType == 'c') {   // bcp -c  
      pColTerm = (BYTE*)ColTerm;  
      pRowTerm = (BYTE*)RowTerm;  
      cbColTerm = 1;  
      cbRowTerm = 2;  
      bulkmode = BCP_OUT_CHARACTER_MODE;  
   }  
   else  
      if(BCPType == 'w') {   // bcp -w  
         pColTerm = (BYTE*)wColTerm;  
         pRowTerm = (BYTE*)wRowTerm;  
         cbColTerm = 2;  
         cbRowTerm = 4;  
         bulkmode = BCP_OUT_WIDE_CHARACTER_MODE;  
      }  
      else  
         if (BCPType == 'n')   // bcp -n  
            bulkmode = BCP_OUT_NATIVE_MODE;  
         else  
            if (BCPType == 'N')   // bcp -n  
               bulkmode = BCP_OUT_NATIVE_TEXT_MODE;  
            else {  
               printf("unknown bcp mode\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            hr = g_pIBcpSession->BCPSetBulkMode(bulkmode, pColTerm, cbColTerm, pRowTerm, cbRowTerm);  
            if (FAILED(hr)) {  
               printf("BCPSetBulkMode failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
  
            // set queryout TSQL statement  
            hr = g_pIBcpSession->BCPControl(BCP_OPTION_HINTS, pszQureryOut);  
            if (FAILED(hr)) {  
               printf("BCPControl failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            // bcp copy  
            DBROWCOUNT nRowsInserted = 0;  
            hr = g_pIBcpSession->BCPExec(&nRowsInserted);  
            if (FAILED(hr)) {  
               printf("BCPExec failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            printf("bcp done\n");  
            OLEDBCleanUp();  
            return true;  
}  
  
int main() {  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -c test', 1,2") , 'c', L"bcpc.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -w test', 1,2") , 'w', L"bcpw.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -c test', 1,2") , 'n', L"bcpn.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -w test', 1,2") , 'N', L"bcp_N.dat");  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession2 &#40;OLE DB&#41;](ibcpsession2-ole-db.md)  
  
  
