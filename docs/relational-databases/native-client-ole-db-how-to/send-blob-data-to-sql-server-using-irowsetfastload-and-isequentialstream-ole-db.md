---
title: BLOB 資料至 SQL、IROWSETFASTLOAD、ISEQUENTIALSTREAM
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: cb022814-a86b-425d-9b24-eaac20ab664e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ea3838f1353318461f6ad725ad31fc372759f4d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303039"
---
# <a name="send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db"></a>使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM 將 BLOB 資料傳送到 SQL SERVER (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  此範例會示範如何使用 IRowsetFastLoad 來串流處理每個資料列中不同長度的 BLOB 資料。  
  
 根據預設，這個範例會示範如何使用 IRowsetFastLoad，透過正規繫結傳送每個資料列中不同長度的 BLOB 資料。 內嵌 BLOB 資料必須配合可用的記憶體。 這個方法在 BLOB 資料的大小為數 MB 時效果最好，因為沒有額外的資料流負荷。 如果資料的大小多於數 MB，尤其是當資料無法以區塊的方式使用時，則資料流的效果較佳。  
  
 在原始程式碼中，當您取消註解 #define USE_ISEQSTREAM 時，此範例會使用 ISequentialStream。 範例中定義了資料流實作，而且只要變更 MAX_BLOB，即可傳送任何大小的 BLOB 資料。 資料流資料並不需要配合記憶體或以單一區塊使用。 您可以使用 IRowsetFastLoad::InsertRow 來呼叫此提供者。 請使用 IRowsetFastLoad::InsertRow，將指標和可從資料流讀取的資料量傳送至資料緩衝區中的資料流實作 (rgBinding.obValue 位移)。 在繫結進行時，某些提供者可能不需要知道資料的長度。 在此例中，繫結中可以省略長度。  
  
 此範例不會使用提供者的資料流介面來將資料寫入提供者， 而會將指標傳送給資料流物件，提供者會取用該指標來讀取資料。 一般而言，Microsoft 提供者 (SQLOLEDB 和 SQLNCLI) 會以 1024 位元組的區塊從物件讀取資料，直到所有資料都經過處理。 SQLOLEDB 或 SQLNCLI 都沒有完整的實作，無法讓取用者將資料寫入至提供者的資料流物件。 只有零長度的資料可以透過提供者的資料流物件傳送。  
  
 取用者實作的 ISequentialStream 物件可和資料列集資料 (IRowsetChange::InsertRow、IRowsetChange::SetData) 搭配使用，也可以透過將參數繫結為 DBTYPE_IUNKNOWN 的方式，與參數搭配使用。  
  
 因為 DBTYPE_IUNKNOWN 會在繫結中指定為資料類型，所以必須符合資料行或目標參數的類型。 從資料列介面透過 ISequentialStream 傳送資料時，不能進行轉換。 對於參數，您應該避免使用 ICommandWithParameters::SetParameterInfo，並指定不同的類別來強制執行轉換；這項作業需要提供者在本機快取所有的 BLOB 資料，以便在傳送到 SQL Server 之前加以轉換。 快取大量的 BLOB 並在本機進行轉換無法提供良好的效能。  
  
 如需詳細資訊，請參閱 [BLOB 與 OLE 物件](../../relational-databases/native-client-ole-db-blobs/blobs-and-ole-objects.md)。  
  
> [!IMPORTANT]  
>  盡可能使用 Windows 驗證。 如果無法使用 Windows 驗證，請提示使用者在執行階段輸入認證。 請避免將認證儲存在檔案中。 如果您必須保存認證，您應該使用[Win32 加密 API](https://go.microsoft.com/fwlink/?LinkId=64532)將它們加密。  
  
## <a name="example"></a>範例  
 執行第一個 ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 程式碼清單，以建立應用程式所使用的資料表。  
  
 使用 ole32.lib oleaut32.lib 編譯並執行下列 C++ 程式碼清單。 這個應用程式會連接到電腦的預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 在某些 Windows 作業系統上，您必須將 (localhost) 或 (local) 變更為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。 若要連線到具名執行個體，請將連接字串從 L"(local)" 變更為 L"(local)\\\name"，其中 name 是具名執行個體。 根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 會安裝至具名執行個體。 請確認您的 INCLUDE 環境變數包含的目錄內含 sqlncli.h。  
  
 執行第三個 ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 程式碼清單，以刪除應用程式所使用的資料表。  
  
```sql
use master  
create table fltest(col1 int, col2 int, col3 image)  
```  
  
```cpp
// compile with: ole32.lib oleaut32.lib  
#include <windows.h>  
  
#define DBINITCONSTANTS   // Must be defined to initialize constants in oledb.h  
#define INITGUID                
  
#include <sqloledb.h>  
#include <oledb.h>  
#include <msdasc.h>  
#include <stdio.h>  
#include <stdlib.h>  
#include <conio.h>  
  
#define MAX_BLOB  200   // For stream binding this can be any size, but for inline it must fit in memory  
#define MAX_ROWS  100  
  
#define SAFE_RELEASE(p) { \  
   if (p) { \  
      (p)->Release(); \  
      (p)=NULL; \  
   } \  
}  
  
#ifdef USE_ISEQSTREAM  
// ISequentialStream implementation for streaming data  
class MySequentialStream : public ISequentialStream {  
  
private:  
   ULONG m_ulRefCount;  
   ULONG m_ulBufSize;  
   ULONG m_ulReadSize;  
   ULONG m_ulBytesLeft;  
   ULONG m_ulReadPos;  
   BYTE * m_pSrcData;  
   BYTE * m_pReadPtr;  
   BOOL m_fWasRead;  
  
public:  
  
   MySequentialStream() {  
      m_ulRefCount = 1;  
      m_ulBufSize = 0;  
      m_ulReadSize = 0;  
      m_ulBytesLeft = 0;  
      m_ulReadPos = 0;  
      m_pSrcData = NULL;  
      m_pReadPtr = NULL;  
      m_fWasRead = FALSE;  
   }  
  
   ~MySequentialStream() {}  
  
   virtual ULONG STDMETHODCALLTYPE AddRef() {  
      return ++m_ulRefCount;  
   }  
  
   virtual ULONG STDMETHODCALLTYPE Release() {  
      --m_ulRefCount;  
      if (m_ulRefCount == 0) {  
         delete this;  
         return 0;  
      }  
      return m_ulRefCount;  
   }  
  
   virtual HRESULT STDMETHODCALLTYPE QueryInterface(REFIID riid, void ** ppvObj) {  
      if (!ppvObj)  
         return E_INVALIDARG;  
      else  
         *ppvObj = NULL;  
  
      if (riid != IID_ISequentialStream && riid != IID_IUnknown)  
         return E_NOINTERFACE;  
  
      AddRef();  
      *ppvObj = this;  
      return S_OK;  
   }  
  
   HRESULT Init(const void * pSrcData, const ULONG ulBufSize, const ULONG ulReadSize) {  
      if (NULL == pSrcData)  
         return E_INVALIDARG;  
  
      // Data length must be non-zero  
      if (0 == ulBufSize)  
         return E_INVALIDARG;  
  
      m_ulBufSize = ulBufSize;  
      m_ulReadSize = ulReadSize;  
      m_pSrcData = (BYTE *)pSrcData;  
      m_pReadPtr = m_pSrcData;  
      m_ulBytesLeft = m_ulReadSize;  
      m_ulReadPos = 0;  
      m_fWasRead = FALSE;  
  
      return S_OK;  
   }  
  
   // Can't write data to SQL Server providers (SQLOLEDB/SQLNCLI).  Instead, they read from our object.  
   virtual HRESULT STDMETHODCALLTYPE Write(const void *, ULONG, ULONG * ) {  
      return E_NOTIMPL;  
   }  
  
   // This implementation simply copies data from the source buffer in whatever size requested.  
   // But you can do anything here such as reading from a file, reading from a different rowset, stream, etc.  
   virtual HRESULT STDMETHODCALLTYPE Read(void * pv, ULONG cb, ULONG * pcbRead) {  
      ULONG ulBytesWritten = 0;  
      ULONG ulCBToWrite = cb;  
      ULONG ulCBToCopy;  
      BYTE * pvb = (BYTE *)pv;  
  
      m_fWasRead = TRUE;  
  
      if (NULL == m_pSrcData)  
         return E_FAIL;  
  
      if (NULL == pv)  
         return STG_E_INVALIDPOINTER;  
  
      while (ulBytesWritten < ulCBToWrite && m_ulBytesLeft) {  
         // Make sure we don't write more than our max read size or the size they asked for  
         ulCBToCopy = min(m_ulBytesLeft, cb);  
  
         // Make sure we don't read past the end of the internal buffer  
         ulCBToCopy = min(m_ulBufSize - m_ulReadPos, ulCBToCopy);  
  
         memcpy(pvb, m_pReadPtr + m_ulReadPos, ulCBToCopy);  
         pvb += ulCBToCopy;  
         ulBytesWritten += ulCBToCopy;  
         m_ulBytesLeft -= ulCBToCopy;  
         cb -= ulCBToCopy;  
  
         // Wrap reads around the src buffer  
         m_ulReadPos += ulCBToCopy;  
         if (m_ulReadPos >= m_ulBufSize)  
            m_ulReadPos = 0;  
      }  
  
      if (pcbRead)  
         *pcbRead = ulBytesWritten;  
  
      return S_OK;  
   }  
};  
  
#endif // USE_ISEQSTREAM  
  
HRESULT SetFastLoadProperty(IDBInitialize * pIDBInitialize) {  
   HRESULT hr = S_OK;  
   IDBProperties * pIDBProps = NULL;  
   DBPROP rgProps[1];  
   DBPROPSET PropSet;  
  
   VariantInit(&rgProps[0].vValue);  
  
   rgProps[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgProps[0].colid = DB_NULLID;  
   rgProps[0].vValue.vt = VT_BOOL;  
   rgProps[0].dwPropertyID = SSPROP_ENABLEFASTLOAD;  
  
   rgProps[0].vValue.boolVal = VARIANT_TRUE;  
  
   PropSet.rgProperties = rgProps;  
   PropSet.cProperties = 1;  
   PropSet.guidPropertySet = DBPROPSET_SQLSERVERDATASOURCE;  
  
   if (SUCCEEDED(hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (LPVOID *)&pIDBProps))) {  
      hr = pIDBProps->SetProperties(1, &PropSet);  
   }  
  
   VariantClear(&rgProps[0].vValue);   
  
   if (pIDBProps)  
      pIDBProps->Release();  
  
   return hr;  
}  
  
void wmain() {  
   // Setup the initialization options  
   ULONG cProperties = 0;  
   DBPROP rgProperties[10];  
   ULONG cPropSets = 0;  
   DBPROPSET rgPropSets[1];  
   LPWSTR pwszProgID = L"SQLOLEDB";  
   LPWSTR pwszDataSource = NULL;  
   LPWSTR pwszUserID = NULL;  
   LPWSTR pwszPassword = NULL;  
   LPWSTR pwszProviderString = L"server=(local);trusted_connection=yes;";  
  
   IDBInitialize * pIDBInitialize = NULL;  
   IDBCreateSession * pIDBCrtSess = NULL;  
   IOpenRowset * pIOpenRowset = NULL;  
   IDBCreateCommand * pIDBCrtCmd = NULL;  
   ICommandText * pICmdText = NULL;  
   IAccessor * pIAccessor = NULL;  
   IRowsetFastLoad * pIRowsetFastLoad = NULL;  
   IDBProperties * pIDBProperties = NULL;  
   DBBINDING rgBinding[3];  
   DBBINDSTATUS rgStatus[3];  
   ULONG ulOffset = 0;  
   HACCESSOR hAcc = DB_NULL_HACCESSOR;  
   BYTE * pData = NULL;  
   ULONG iRow = 0;  
   LPWSTR pwszTableName = L"fltest";  
   DBID TableID;  
  
   HRESULT hr;  
  
#ifdef USE_ISEQSTREAM  
   BYTE bSrcBuf[1024];   // A buffer to hold our data for streaming  
   memset((void *)&bSrcBuf, 0xAB, sizeof(bSrcBuf));   // Stream data value 0xAB  
   MySequentialStream * pMySeqStream = new MySequentialStream();  
   DBOBJECT MyObject = {STGM_READ, IID_ISequentialStream};   // NULL pObject implies STGM_READ and IID_IUnknown, but not recommended  
#endif  
  
   memset(rgBinding, 0, ( sizeof(rgBinding) / sizeof(rgBinding[0])) * sizeof(DBBINDING) );  
   TableID.eKind = DBKIND_NAME;  
   TableID.uName.pwszName = pwszTableName;  
  
   // Col1  
   rgBinding[0].iOrdinal = 1;  
   rgBinding[0].wType = DBTYPE_I4;  
   rgBinding[0].obStatus = ulOffset;  
   ulOffset+=sizeof(DBSTATUS);  
   rgBinding[0].obLength = ulOffset;  
   ulOffset+=sizeof(DBLENGTH);  
   rgBinding[0].obValue = ulOffset;  
   ulOffset += sizeof(LONG);  
   rgBinding[0].cbMaxLen = sizeof(LONG);  
   rgBinding[0].dwPart = DBPART_VALUE | DBPART_STATUS | DBPART_LENGTH;  
   rgBinding[0].eParamIO = DBPARAMIO_NOTPARAM;  
   rgBinding[0].dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
  
   //Col2  
   rgBinding[1].iOrdinal = 2;  
   rgBinding[1].wType = DBTYPE_I4;  
   rgBinding[1].obStatus = ulOffset;  
   ulOffset+=sizeof(DBSTATUS);  
   rgBinding[1].obLength = ulOffset;  
   ulOffset+=sizeof(DBLENGTH);  
   rgBinding[1].obValue = ulOffset;  
   ulOffset += sizeof(LONG);  
   rgBinding[1].cbMaxLen = sizeof(LONG);  
   rgBinding[1].dwPart = DBPART_VALUE | DBPART_STATUS | DBPART_LENGTH;  
   rgBinding[1].eParamIO = DBPARAMIO_NOTPARAM;  
   rgBinding[1].dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
  
   //Col3  
   rgBinding[2].iOrdinal = 3;  
   rgBinding[2].obStatus = ulOffset;  
   ulOffset+=sizeof(DBSTATUS);  
   rgBinding[2].obLength = ulOffset;  
   ulOffset+=sizeof(DBLENGTH);  
   rgBinding[2].obValue = ulOffset;  
   rgBinding[2].dwPart = DBPART_VALUE | DBPART_STATUS | DBPART_LENGTH;   // DBPART_LENGTH not needed for providers that don't require length  
   rgBinding[2].eParamIO = DBPARAMIO_NOTPARAM;  
   rgBinding[2].dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
  
#ifdef USE_ISEQSTREAM  
   rgBinding[2].wType = DBTYPE_IUNKNOWN;  
   ulOffset += sizeof(ISequentialStream *);   // Technically should be sizeof(MySequentialStream *), but who's counting?  
   rgBinding[2].cbMaxLen = sizeof(ISequentialStream *);  
   rgBinding[2].pObject = &MyObject;  
#else  
   rgBinding[2].wType = DBTYPE_BYTES;  
   ulOffset += MAX_BLOB;  
   rgBinding[2].cbMaxLen = MAX_BLOB;  
#endif  
  
   // Set init props  
   for ( ULONG i = 0 ; i < sizeof(rgProperties) / sizeof(rgProperties[0]) ; i++ )  
      VariantInit(&rgProperties[i].vValue);  
  
   // Obtain the provider's clsid  
   CLSID clsidProv;  
   hr = CLSIDFromProgID(pwszProgID, &clsidProv);  
  
   // Get our initial connection  
   CoInitialize(NULL);  
  
   if (SUCCEEDED(hr))  
      hr = CoCreateInstance(clsidProv, NULL, CLSCTX_ALL, IID_IDBInitialize,(void **)&pIDBInitialize);  
  
   if (SUCCEEDED(hr))  
      hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);  
  
   // DBPROP_INIT_DATASOURCE  
   if (pwszDataSource) {  
      rgProperties[cProperties].dwPropertyID    = DBPROP_INIT_DATASOURCE;  
      rgProperties[cProperties].dwOptions       = DBPROPOPTIONS_REQUIRED;  
      rgProperties[cProperties].dwStatus        = DBPROPSTATUS_OK;  
      rgProperties[cProperties].colid           = DB_NULLID;  
      rgProperties[cProperties].vValue.vt       = VT_BSTR;  
      V_BSTR(&rgProperties[cProperties].vValue) = SysAllocString(pwszDataSource);                 
      cProperties++;  
   }  
  
   // DBPROP_AUTH_USERID  
   if (pwszUserID) {  
      rgProperties[cProperties].dwPropertyID    = DBPROP_AUTH_USERID;  
      rgProperties[cProperties].dwOptions       = DBPROPOPTIONS_REQUIRED;  
      rgProperties[cProperties].dwStatus        = DBPROPSTATUS_OK;  
      rgProperties[cProperties].colid           = DB_NULLID;  
      rgProperties[cProperties].vValue.vt       = VT_BSTR;  
      V_BSTR(&rgProperties[cProperties].vValue) = SysAllocString(pwszUserID);  
      cProperties++;  
   }  
  
   // DBPROP_AUTH_PASSWORD  
   if (pwszPassword) {  
      rgProperties[cProperties].dwPropertyID    = DBPROP_AUTH_PASSWORD;  
      rgProperties[cProperties].dwOptions       = DBPROPOPTIONS_REQUIRED;  
      rgProperties[cProperties].dwStatus        = DBPROPSTATUS_OK;  
      rgProperties[cProperties].colid           = DB_NULLID;  
      rgProperties[cProperties].vValue.vt       = VT_BSTR;  
      V_BSTR(&rgProperties[cProperties].vValue) = SysAllocString(pwszPassword);  
      cProperties++;  
   }  
  
   // DBPROP_INIT_PROVIDERSTRING  
   if (pwszProviderString) {  
      rgProperties[cProperties].dwPropertyID    = DBPROP_INIT_PROVIDERSTRING;  
      rgProperties[cProperties].dwOptions       = DBPROPOPTIONS_REQUIRED;  
      rgProperties[cProperties].dwStatus        = DBPROPSTATUS_OK;  
      rgProperties[cProperties].colid           = DB_NULLID;  
      rgProperties[cProperties].vValue.vt       = VT_BSTR;  
      V_BSTR(&rgProperties[cProperties].vValue) = SysAllocString(pwszProviderString);  
      cProperties++;  
   }  
  
   if (cProperties) {  
      rgPropSets[cPropSets].cProperties = cProperties;  
      rgPropSets[cPropSets].rgProperties = rgProperties;  
      rgPropSets[cPropSets].guidPropertySet = DBPROPSET_DBINIT;  
      cPropSets++;  
   }  
  
   // Initialize  
   if (SUCCEEDED(hr))  
      hr = pIDBProperties->SetProperties(cPropSets, rgPropSets);  
  
   if (SUCCEEDED(hr))  
      hr = pIDBInitialize->Initialize();  
  
   if (SUCCEEDED(hr)) {  
      printf("\tConnected!\r\n");  
   }  
   else  
      printf("Unable to connect\r\n");  
  
   // Set fastload prop  
   if (SUCCEEDED(hr))  
      hr = SetFastLoadProperty(pIDBInitialize);  
  
   if (SUCCEEDED(hr))  
      hr = pIDBInitialize->QueryInterface(IID_IDBCreateSession, (void **)&pIDBCrtSess);  
  
   if (SUCCEEDED(hr))  
      hr = pIDBCrtSess->CreateSession(NULL, IID_IOpenRowset, (IUnknown **)&pIOpenRowset);  
  
   if (SUCCEEDED(hr))  
      hr = pIOpenRowset->OpenRowset(NULL, &TableID, NULL, IID_IRowsetFastLoad, 0, NULL, (IUnknown **)&pIRowsetFastLoad);  
  
   if (SUCCEEDED(hr))  
      hr = pIRowsetFastLoad->QueryInterface(IID_IAccessor, (void **)&pIAccessor);  
  
   if (SUCCEEDED(hr))  
      hr = pIAccessor->CreateAccessor(DBACCESSOR_ROWDATA, 3, rgBinding, ulOffset, &hAcc, (DBBINDSTATUS *)&rgStatus);  
  
   if (SUCCEEDED(hr)) {  
      pData = (BYTE *)malloc(ulOffset);  
  
      for (iRow = 0 ; iRow < MAX_ROWS ; iRow++) {  
         // Column 1 data          
         *(DBSTATUS *)(pData + rgBinding[0].obStatus) = DBSTATUS_S_OK;  
         *(DBLENGTH *)(pData + rgBinding[0].obLength) = 1234567;   // Ignored for I4 data  
         *(LONG *)(pData + rgBinding[0].obValue) = iRow;  
  
         // Column 2 data          
         *(DBSTATUS *)(pData + rgBinding[1].obStatus) = DBSTATUS_S_OK;  
         *(DBLENGTH *)(pData + rgBinding[1].obLength) = 1234567;   // Ignored for I4 data  
         *(LONG *)(pData + rgBinding[1].obValue) = iRow + 1;  
  
         // Column 3 data          
         *(DBSTATUS *)(pData + rgBinding[2].obStatus) = DBSTATUS_S_OK;  
         *(DBLENGTH *)(pData + rgBinding[2].obLength) = MAX_BLOB/(iRow + 1);   // Not needed for providers that don't require length  
#ifdef USE_ISEQSTREAM  
         // DBLENGTH is used to tell the provider how much BLOB data to expect from the stream, not required  
         // if provider supports sending data without length  
         *(ISequentialStream **)(pData+rgBinding[2].obValue) = (ISequentialStream *)pMySeqStream;   
         pMySeqStream->Init((void *)&bSrcBuf, sizeof(bSrcBuf), MAX_BLOB / (iRow + 1));   // Here we set the size we will let the provider read  
         pMySeqStream->AddRef();   // The provider releases the object, so we addref it so it doesn't get destructed  
#else  
         memset(pData + rgBinding[2].obValue, 0, MAX_BLOB);   // Not strictly necessary  
         memset(pData + rgBinding[2].obValue, 0x23, MAX_BLOB / (iRow + 1));   
#endif  
         if (SUCCEEDED(hr))  
            hr = pIRowsetFastLoad->InsertRow(hAcc, pData);  
      }  
   }  
  
   if (SUCCEEDED(hr))  
      hr = pIRowsetFastLoad->Commit(TRUE);  
  
   if (hAcc)  
      pIAccessor->ReleaseAccessor(hAcc, NULL);  
  
   SAFE_RELEASE(pIDBInitialize);  
   SAFE_RELEASE(pIDBCrtSess);  
   SAFE_RELEASE(pIOpenRowset);  
   SAFE_RELEASE(pIDBCrtCmd);  
   SAFE_RELEASE(pICmdText);  
   SAFE_RELEASE(pIAccessor);  
   SAFE_RELEASE(pIRowsetFastLoad);  
   SAFE_RELEASE(pIDBProperties);  
#ifdef USE_ISEQSTREAM  
   SAFE_RELEASE(pMySeqStream);  
#endif  
  
   if (pData)  
      free(pData);  
  
   CoUninitialize();  
}  
```  
  
```sql
use master  
drop table fltest  
```  
  
  
