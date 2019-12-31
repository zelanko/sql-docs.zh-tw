---
title: 使用 OLE DB 執行 Updategram （SQLXML）
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- ICommandStream interface
- updategrams [SQLXML], OLE DB
- OLE DB, SQLXML
- executing updategrams [SQLXML]
ms.assetid: 4154c590-1541-49d0-8117-4ddf2ce5ccba
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 754db698b7c82a64f66cbb7a4df43bd4127413d1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241275"
---
# <a name="executing-an-updategram-by-using-ole-db-sqlxml-40"></a>使用 OLE DB 執行 Updategram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主題提供 usingOLE DB 的工作範例，以執行 updategram。  
  
## <a name="using-icommandstream-to-set-an-xml-command"></a>使用 ICommandStream 來設定 XML 命令  
 OLE DB （版本2.6 或更新版本） ICommandStream 介面會傳遞命令做為資料流程物件，而不是字串。  
  
 此介面可以讓命令使用 XML 剖析器所了解的任何編碼。 呼叫 ICommand：： Execute 時，會直接從資料流程讀取命令文字，而不需要轉換。 因此，使用 ICommandStream 介面執行 XML 命令會更有效率。  
  
### <a name="setting-xml-as-a-command-using-icommandstream-and-retrieving-the-results-as-an-xml-document"></a>使用 ICommandStream 將 XML 設定為命令並且將結果擷取為 XML 文件  
 ICommandStream 介面可用來將 XML 檔設定為命令，並將結果當做 XML 檔來抓取。  
  
#### <a name="executing-templates-with-xpath-queries"></a>執行具有 XPath 查詢的範本  
 下列包含 XPath 查詢的 XML 範本會指定為使用 ICommandStream 的命令：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:xpath-query mapping-schema="Schema.xml">Person.Contact</sql:xpath-query>  
</ROOT>  
```  
  
 範本中的 XPath 查詢會根據下列的對應結構描述執行：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data" xmlns:dt="urn:schemas-microsoft-com:datatypes" xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Person.Contact" >  
<AttributeType name="ContactID" />  
<AttributeType name="FirstName" />  
<AttributeType name="LastName" />  
<attribute type="ContactID" />  
<attribute type="FirstName" />  
<attribute type="LastName" />  
</ElementType>  
</Schema>  
```  
  
 此查詢會傳回所有的員工元素。 使用預設對應時， ** \<Person. Contact>** 元素會對應到 AdventureWorks 資料庫中的 person. contact 資料表。  
  
###### <a name="to-set-xml-as-a-command-and-retrieving-result-as-an-xml-document"></a>將 XML 設定為命令並且將結果擷取為 XML 文件  
  
1.  初始化並建立資料庫連接。  
  
2.  取得 ICommand 上的 ICommandStream 介面。  
  
3.  設定必要的命令屬性。 在此範例中，提供者特定的屬性 SSPROP_STREAM_BASEPATH 是設為儲存對應結構描述和範本檔案的目錄。  
  
4.  請使用 ICommandStream：： SetCommandStream 來指定命令資料流程。 此範例執行的 XML 範本是讀取自檔案。 這項功能在執行大型 XML 範本時相當有用。  
  
5.  使用 ICommand：： Execute 執行 XML 命令，並要求 IID_ISequentialStream 介面識別碼。  
  
6.  處理結果。 在此範例中，讀取自資料流的 XML 會顯示在畫面中。  
  
    ```  
    void InitializeAndEstablishConnection();  
    void SetCommandProperties();  
    void ProcessResultSet();  
  
    #define UNICODE  
    #define _UNICODE  
    #define DBINITCONSTANTS  
    #define INITGUID  
  
    #include <stdio.h>  
    #include <tchar.h>  
    #include <stddef.h>  
    #include <windows.h>  
    #include <iostream.h>  
    #include <oledb.h>  
    #include <SQLOLEDB.h>  
  
    class CSequentialStream : public ISequentialStream  
    {  
       private:     
          ULONG       m_cRef;              // reference count  
          HANDLE      m_hFile;         // handle to the file  
          LPWSTR      m_wszFileName;      // the file name  
  
       public:  
          CSequentialStream( LPWSTR );  
          virtual ~CSequentialStream();  
  
          // IUnknown Methods  
          STDMETHODIMP_(ULONG)    AddRef();  
          STDMETHODIMP_(ULONG)    Release();  
          STDMETHODIMP QueryInterface( REFIID, LPVOID* );  
  
          // ISequentialStream Methods  
          STDMETHODIMP Read(   
                /* [out] */ void __RPC_FAR*,  
                /* [in]  */ ULONG,  
                /* [out] */ ULONG __RPC_FAR* );  
  
          STDMETHODIMP Write(   
                /* [in] */ const void __RPC_FAR*,  
                /* [in] */ ULONG,  
                /* [out]*/ ULONG __RPC_FAR* );  
    };  
  
    IDBInitialize*       pIDBInitialize     = NULL;  
    IDBProperties*       pIDBProperties     = NULL;  
    IDBCreateSession*    pIDBCreateSession  = NULL;  
    IDBCreateCommand*    pIDBCreateCommand  = NULL;  
    ICommand*            pICommand          = NULL;  
    ICommandStream*      pICommandStream    = NULL;  
    ICommandProperties*    pICommandProperties = NULL;  
    IColumnsInfo*        pIColumnsInfo      = NULL;  
    ISequentialStream*    pIXMLOutput      = NULL;  
    DBCOLUMNINFO*        pDBColumnInfo      = NULL;  
    IAccessor*           pIAccessor        =  NULL;  
    DBPROP               InitProperties[4];  
    DBPROPSET            rgInitPropSet[1];  
    ULONG                i, j;  
    HRESULT              hr;  
    LONG                 cNumRows = 0;  
    ULONG                lNumCols;  
    WCHAR*               pStringsBuffer;  
    DBBINDING*           pBindings;  
    ULONG                ConsumerBufColOffset = 0;  
    HACCESSOR            hAccessor;  
    ULONG                lNumRowsRetrieved;  
    HROW                 hRows[10];  
    HROW*                pRows = &hRows[0];  
    BYTE*                pBuffer;  
    CSequentialStream    XMLInput( L"Query.xml" );  
  
    CSequentialStream::CSequentialStream  
    (  
       LPWSTR      wszFileName  
    )  
    :  
       m_cRef( 0 ),  
       m_hFile( NULL ),  
       m_wszFileName( NULL )  
    {  
        // The constructor AddRefs.  
        AddRef();  
  
       // Allocate memory for the file name.  
       m_wszFileName = (LPWSTR) CoTaskMemAlloc( ( wcslen( wszFileName ) + 1 ) * 2 );  
  
       // Copy the file name.  
       wcscpy( m_wszFileName, wszFileName );  
    }  
  
    CSequentialStream::~CSequentialStream  
    (  
    )  
    {  
       // Free any allocated memory.  
       if( m_wszFileName )  
          CoTaskMemFree( m_wszFileName );  
  
       // Close the file.  
       if( m_hFile )  
          CloseHandle( m_hFile );  
    }  
  
    ULONG      
    CSequentialStream::AddRef  
    (  
    )  
    {  
        return ++m_cRef;  
    }  
  
    ULONG  
    CSequentialStream::Release()  
    {  
        if(--m_cRef)  
            return m_cRef;  
  
        delete this;  
        return 0;  
    }  
  
    HRESULT   
    CSequentialStream::QueryInterface  
    (     
       REFIID riid,   
       void** ppv  
    )  
    {  
        *ppv = NULL;  
  
        if (riid == IID_IUnknown)  
            *ppv = this;  
  
        if (riid == IID_ISequentialStream)  
            *ppv = this;  
  
        if(*ppv)  
        {  
            ((IUnknown*)*ppv)->AddRef();  
            return S_OK;  
        }  
  
        return E_NOINTERFACE;  
    }  
  
    HRESULT   
    CSequentialStream::Read  
    (  
       void *pv,   
       ULONG cb,   
       ULONG* pcbRead  
    )  
    {  
       ULONG   cBytesRead = 0;  
  
        // Parameter checking.  
        if(pcbRead)  
            *pcbRead = 0;  
  
        if(!pv)  
            return STG_E_INVALIDPOINTER;  
  
        if(cb == 0)  
            return S_OK;  
  
       // Do we need to open the file?  
       if( m_hFile == NULL )  
       {  
          // Open the file.  
          m_hFile = CreateFile( m_wszFileName, GENERIC_READ, 0, NULL, OPEN_EXISTING, 0, NULL );  
  
          // If the file failed to open, return E_FAIL.  
          if( m_hFile == INVALID_HANDLE_VALUE )  
             return E_FAIL;  
       }  
  
       // Clear the buffer.  
       ZeroMemory( pv, cb );  
  
       // Read cb bytes from the stream.  
       if( !ReadFile( m_hFile, pv, cb, &cBytesRead, NULL ) )  
          return E_FAIL;  
  
       // Inform the user of how many bytes to read.  
       if( NULL != pcbRead )   
          *pcbRead = cBytesRead;  
  
        if(cb != cBytesRead)  
            return S_FALSE;   
  
        return S_OK;  
    }  
  
    HRESULT   
    CSequentialStream::Write  
    (  
       const void *pv,   
       ULONG cb,   
       ULONG* pcbWritten  
    )  
    {  
       // For this example, only a read-only stream is needed.  
       return STG_E_CANTSAVE;  
    }  
  
    void main()   
    {  
       // Call a function to initialize and establish a connection.   
        InitializeAndEstablishConnection();  
  
        // Create a session object.  
        if(FAILED(pIDBInitialize->QueryInterface(  
                                    IID_IDBCreateSession,  
                                    (void**) &pIDBCreateSession)))  
        {  
            cout << "Failed to obtain IDBCreateSession interface.\n";  
        }  
  
        if(FAILED(pIDBCreateSession->CreateSession(  
                                         NULL,   
                                         IID_IDBCreateCommand,   
                                         (IUnknown**) &pIDBCreateCommand)))  
        {  
            cout << "pIDBCreateSession->CreateSession failed.\n";  
        }  
  
        // Access the ICommand interface.  
        if(FAILED(pIDBCreateCommand->CreateCommand(  
                                        NULL,   
                                        IID_ICommand,   
                                        (IUnknown**) &pICommand)))  
        {  
            cout << "Failed to access ICommand interface.\n";  
        }  
  
       // Get an ICommandStream interface.  
       if(FAILED(pICommand->QueryInterface( IID_ICommandStream, (void**) &pICommandStream)))  
       {  
          cout << "Failed to get an ICommandStream interface.\n";  
       }  
  
       // Get an ICommandProperties interface.  
       if(FAILED(pICommand->QueryInterface( IID_ICommandProperties, (void**) &pICommandProperties)))  
       {  
          cout << "Failed to get an ICommandProperties interface.\n";  
       }  
  
       // Set the command properties.  
       SetCommandProperties();  
  
        // Use SetCommandStream() to specify the command stream.  
        if(FAILED(pICommandStream->SetCommandStream(IID_ISequentialStream, DBGUID_DEFAULT, (ISequentialStream*) &XMLInput )))  
        {  
            cout << "Failed to set command stream.\n";  
        }  
  
        // Execute the command.  
        if(FAILED(hr = pICommand->Execute(NULL,   
                                        IID_ISequentialStream,   
                                        NULL,   
                                        &cNumRows,   
                                        (IUnknown **) &pIXMLOutput )))  
        {  
            cout << "Failed to execute command.\n";  
        }  
  
        // Process the result set.  
        ProcessResultSet();   
  
        // Free memory.  
       if( pIXMLOutput )  
          pIXMLOutput->Release();  
       pICommandProperties->Release();  
       pICommandStream->Release();  
        pICommand->Release();  
        pIDBCreateCommand->Release();  
        pIDBCreateSession->Release();  
  
        if(FAILED(pIDBInitialize->Uninitialize()))  
        {  
            /*Uninitialize is not required, but it fails if an interface  
            has not been released. This can be used for debugging.  
            cout << "Problem uninitializing.\n"; */  
        } // endif.  
        pIDBInitialize->Release();  
  
        // Release the COM library.  
        CoUninitialize();  
    };  
  
    //--------------------------------------------------------------------  
    void InitializeAndEstablishConnection()  
    {      
        // Initialize the COM library.  
        CoInitialize(NULL);  
  
        // Obtain access to the SQLOLEDB Provider.  
        hr = CoCreateInstance(CLSID_SQLOLEDB,   
                              NULL,   
                              CLSCTX_INPROC_SERVER,  
                              IID_IDBInitialize,   
                              (void **) &pIDBInitialize);  
        if(FAILED(hr))  
        {  
            printf("Failed to get IDBInitialize interface.\n");  
        } // end if  
  
        /*  
        Initialize the property values needed   
        to establish the connection.  
        */  
        for(i = 0; i < 4; i++)   
            VariantInit(&InitProperties[i].vValue);  
  
        // Server name.  
        InitProperties[0].dwPropertyID  = DBPROP_INIT_DATASOURCE;  
        InitProperties[0].vValue.vt     = VT_BSTR;  
        InitProperties[0].vValue.bstrVal=   
                                SysAllocString(L"Server");  
        InitProperties[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[0].colid         = DB_NULLID;  
  
    // Database.  
        InitProperties[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
        InitProperties[1].vValue.vt     = VT_BSTR;  
        InitProperties[1].vValue.bstrVal= SysAllocString(L"northwind");  
        InitProperties[1].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[1].colid         = DB_NULLID;  
  
    // Username (login).  
        InitProperties[2].dwPropertyID  = DBPROP_AUTH_USERID;   
        InitProperties[2].vValue.vt     = VT_BSTR;  
        InitProperties[2].vValue.bstrVal= SysAllocString(L"Login");  
        InitProperties[2].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[2].colid         = DB_NULLID;  
  
    // Password.  
    //    InitProperties[3].dwPropertyID  = DBPROP_AUTH_PASSWORD;   
    //    InitProperties[3].vValue.vt     = VT_BSTR;  
    //    InitProperties[3].vValue.bstrVal= SysAllocString(L"Password");  
    //    InitProperties[3].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    //    InitProperties[3].colid         = DB_NULLID;  
  
        /*  
        Now that the properties are set, construct the DBPROPSET structure.  
        (rgInitPropSet). The DBPROPSET structure is used to pass an array   
        of DBPROP structures (InitProperties) to the SetProperties method.  
        */  
        rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
    //  rgInitPropSet[0].cProperties    = 4;  
        rgInitPropSet[0].cProperties    = 3;  
        rgInitPropSet[0].rgProperties   = InitProperties;  
  
        // Set initialization properties.  
        hr = pIDBInitialize->QueryInterface(IID_IDBProperties,   
                                       (void **)&pIDBProperties);  
        if(FAILED(hr))  
        {  
            cout << "Failed to get IDBProperties interface.\n";  
        }  
  
        hr = pIDBProperties->SetProperties(1, rgInitPropSet);   
        if(FAILED(hr))  
        {  
            cout << "Failed to set initialization properties.\n";  
        } // end if  
  
        pIDBProperties->Release();  
  
        // Establish the connection to the data source.  
        if(FAILED(pIDBInitialize->Initialize()))  
        {  
            cout << "Problem establishing connection to the data source.\n";  
        }  
    } // End of InitializeAndEstablishConnection.  
    void SetCommandProperties()  
    {      
    //    for(i = 0; i < 4; i++)   
            VariantInit(&InitProperties[0].vValue);  
  
        // Server name.  
        InitProperties[0].dwPropertyID  = SSPROP_STREAM_BASEPATH;  
        InitProperties[0].vValue.vt     = VT_BSTR;  
        InitProperties[0].vValue.bstrVal=   
                                SysAllocString(L"C:\\MyDir");  
        InitProperties[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[0].colid         = DB_NULLID;  
  
        /*  
        Now that the properties are set, construct the DBPROPSET structure  
        (rgInitPropSet). The DBPROPSET structure is used to pass an array   
        of DBPROP structures (InitProperties) to the SetProperties method.  
        */  
        rgInitPropSet[0].guidPropertySet = DBPROPSET_SQLSERVERSTREAM;  
        rgInitPropSet[0].cProperties    = 1;  
        rgInitPropSet[0].rgProperties   = InitProperties;  
  
        // Set initialization properties.  
        hr = pICommandProperties->SetProperties(1, rgInitPropSet);   
        if(FAILED(hr))  
        {  
            cout << "Failed to set command properties.\n";  
        } // end if  
    } // End of InitializeAndEstablishConnection.  
  
    //--------------------------------------------------------------------  
    // Retrieve and display data resulting from a query.  
    void ProcessResultSet()  
    {  
       CHAR   szBuf[1000];  
       ULONG   ulNumRead;  
       HRESULT   hr;  
  
       if( pIXMLOutput == NULL )  
          return;  
  
       // Read from the stream.  
       ZeroMemory( szBuf, 1000 );  
       while( ( hr = pIXMLOutput->Read( szBuf, 1000, &ulNumRead ) ) == S_OK )  
       {  
          cout << szBuf;  
       }  
    } // Process resultset.  
    ```  
  
#### <a name="passing-parameters-to-templates"></a>將參數傳遞給範本  
 此範例顯示如何將參數值傳遞給 XML 命令。 此 XML 範本會指定為命令：  
  
```  
<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:header><sql:param name='Title'>Mr.</sql:param></sql:header>  
<sql:query>SELECT TOP 20 * FROM Person.Contact  
WHERE Title = @Title  
FOR XML AUTO</sql:query>  
</ROOT>  
```  
  
 範本包含了 SQL 查詢。 查詢需要其參數的值（@Title）。 如果沒有傳遞任何參數值，則會使用預設值 ("Mr.")。  
  
 將參數值傳遞給範本時，必須同時指定參數名稱和值。  
  
 以下為程式碼：  
  
```  
#define UNICODE  
#define _UNICODE  
#define DBINITCONSTANTS  
#define INITGUID  
  
#include <stdio.h>  
#include <tchar.h>  
#include <stddef.h>  
#include <windows.h>  
#include <iostream.h>  
#include "oledb.h"  
#include "SQLOLEDB.h"  
  
HRESULT InitializeAndEstablishConnection(IDBInitialize ** ppIDBInitialize);  
HRESULT SetCommandProperties(ICommand * pICommand);  
HRESULT ProcessResultSet(ISequentialStream * pStreamOutput);  
  
//---------------------------------------------------------------------  
// Structure Definition Section  
//---------------------------------------------------------------------  
struct COLUMNDATA  
{  
    DBLENGTH    dwLength;   // The length of the data field  
    DBSTATUS    dwStatus;   // The status value  
    BYTE        bData[1];   // The start of the data field  
};  
  
class CSequentialStream : public ISequentialStream  
{  
    private:      
        ULONG       m_cRef;             // reference count  
        HANDLE      m_hFile;            // handle to the file  
        LPWSTR      m_wszFileName;      // the file name  
  
    public:  
        CSequentialStream( LPWSTR );  
        virtual ~CSequentialStream();  
  
        // IUnknown Methods  
        STDMETHODIMP_(ULONG)    AddRef();  
        STDMETHODIMP_(ULONG)    Release();  
        STDMETHODIMP QueryInterface( REFIID, LPVOID* );  
  
        // ISequentialStream Methods  
        STDMETHODIMP Read(   
                /* [out] */ void __RPC_FAR*,  
                /* [in]  */ ULONG,  
                /* [out] */ ULONG __RPC_FAR* );  
  
        STDMETHODIMP Write(   
                /* [in] */ const void __RPC_FAR*,  
                /* [in] */ ULONG,  
                /* [out]*/ ULONG __RPC_FAR* );  
};  
  
CSequentialStream::CSequentialStream  
(  
    LPWSTR      wszFileName  
)  
:  
    m_cRef( 0 ),  
    m_hFile( NULL ),  
    m_wszFileName( NULL )  
{  
    // The constructor AddRefs.  
    AddRef();  
  
    // Allocate memory for the file name.  
    m_wszFileName = (LPWSTR) CoTaskMemAlloc( ( wcslen( wszFileName ) + 1 ) * 2 );  
  
    // Copy the file name  
    wcscpy( m_wszFileName, wszFileName );  
}  
  
CSequentialStream::~CSequentialStream  
(  
)  
{  
    // Free any allocated memory.  
    if( m_wszFileName )  
        CoTaskMemFree( m_wszFileName );  
  
    // Close the file.  
    if( m_hFile )  
        CloseHandle( m_hFile );  
}  
  
ULONG      
CSequentialStream::AddRef  
(  
)  
{  
    return ++m_cRef;  
}  
ULONG CSequentialStream::Release()  
{  
    if(--m_cRef)  
        return m_cRef;  
  
    delete this;  
    return 0;  
}  
  
HRESULT CSequentialStream::QueryInterface  
(     
    REFIID riid,   
    void** ppv  
)  
{  
    *ppv = NULL;  
  
    if (riid == IID_IUnknown)  
        *ppv = this;  
  
    if (riid == IID_ISequentialStream)  
        *ppv = this;  
  
    if(*ppv)  
    {  
        ((IUnknown*)*ppv)->AddRef();  
        return S_OK;  
    }  
  
    return E_NOINTERFACE;  
}  
  
HRESULT CSequentialStream::Read  
(  
    void *pv,   
    ULONG cb,   
    ULONG* pcbRead  
)  
{  
    ULONG   cBytesRead = 0;  
  
    // Parameter checking.  
    if(pcbRead)  
        *pcbRead = 0;  
  
    if(!pv)  
        return STG_E_INVALIDPOINTER;  
  
    if(cb == 0)  
        return S_OK;  
  
    // Do we need to open the file?  
    if( m_hFile == NULL )  
    {  
        // Open the file.  
        m_hFile = CreateFile( m_wszFileName, GENERIC_READ, 0, NULL, OPEN_EXISTING, 0, NULL );  
  
        // If we failed to open the file, return E_FAIL.  
        if( m_hFile == INVALID_HANDLE_VALUE )  
            return E_FAIL;  
    }  
  
    // Clear the buffer.  
    ZeroMemory( pv, cb );  
  
    // Read cb bytes from the stream.  
    if( !ReadFile( m_hFile, pv, cb, &cBytesRead, NULL ) )  
        return E_FAIL;  
  
    // Inform the user how many bytes were read.  
    if( NULL != pcbRead )   
        *pcbRead = cBytesRead;  
  
    if(cb != cBytesRead)  
        return S_FALSE;   
  
    return S_OK;  
}  
  
HRESULT CSequentialStream::Write  
(  
    const void *pv,   
    ULONG cb,   
    ULONG* pcbWritten  
)  
{  
    // For purposes of this example, only a read-only stream is needed.  
    return STG_E_CANTSAVE;  
}  
void main()   
{  
    HRESULT                 hr = S_OK;  
    IDBInitialize         * pIDBInitialize          = NULL;  
    IDBCreateSession      * pIDBCreateSession       = NULL;  
    IDBCreateCommand      * pIDBCreateCommand       = NULL;  
    ICommand              * pICommand               = NULL;  
    ICommandStream        * pICommandStream         = NULL;  
    ICommandWithParameters* pICommandWithParameters = NULL;  
    ICommandText          * pICommandText           = NULL;  
    IAccessor             * pIAccessor              = NULL;  
    const ULONG             nParams = 1;  
    DBPARAMS              * pParams                 = NULL;  
    DBPARAMS                params;  
    DBBINDING               acDBBinding[nParams];  
    DBBINDSTATUS            acDBBindStatus[nParams];  
    DBORDINAL               rgParamOrdinals[1];  
    DBPARAMBINDINFO         rgParamBindInfo[1];  
    const WCHAR           * wszParamName =      L"@CategoryName";  
    const WCHAR           * wszDataSourceType = L"DBTYPE_WCHAR";  
    BYTE                    sprocparams[1000];  
    COLUMNDATA            * pCol = (COLUMNDATA *) sprocparams;  
    ISequentialStream     * pStreamOutput       = NULL;  
    DBCOLUMNINFO          * pDBColumnInfo       = NULL;  
    HACCESSOR               hAccessor;  
    CSequentialStream       XMLInput( L"TemplateFile.xml" );  
  
    typedef struct tagSPROCPARAMS  
    {  
        WCHAR CategoryName[25];  
    } SPROCPARAMS;  
  
    CoInitialize(0);  
  
    // Call a function to initialize and establish connection.   
    if (FAILED(hr = InitializeAndEstablishConnection(&pIDBInitialize)))  
        goto Cleanup;  
  
    //Create a session object.  
    if(FAILED(hr = pIDBInitialize->QueryInterface(  
                                IID_IDBCreateSession,  
                                (void**) &pIDBCreateSession)))  
    {  
        cout << "Failed to obtain IDBCreateSession interface.\n";  
        goto Cleanup;  
    }  
  
    if(FAILED(hr = pIDBCreateSession->CreateSession(  
                                     NULL,   
                                     IID_IDBCreateCommand,   
                                     (IUnknown**) &pIDBCreateCommand)))  
    {  
        cout << "pIDBCreateSession->CreateSession failed.\n";  
        goto Cleanup;  
    }  
  
    //Access the ICommand interface.  
    if(FAILED(hr = pIDBCreateCommand->CreateCommand(  
                                    NULL,   
                                    IID_ICommand,   
                                    (IUnknown**) &pICommand)))  
    {  
        cout << "Failed to access ICommand interface.\n";  
        goto Cleanup;  
    }  
  
    // Get an ICommandStream interface  
    if(FAILED(pICommand->QueryInterface( IID_ICommandStream, (void**) &pICommandStream)))  
    {  
        cout << "Failed to get an ICommandStream interface.\n";  
        goto Cleanup;  
    }  
  
    //Use SetCommandStream() to specify the command stream.  
    if(FAILED(hr = pICommandStream->SetCommandStream(IID_ISequentialStream, DBGUID_DEFAULT, (ISequentialStream*) &XMLInput )))  
    {  
        cout << "Failed to set command stream.\n";  
        goto Cleanup;  
    }  
  
    // Set the command properties.  
    if (FAILED(hr = SetCommandProperties(pICommand)))  
        goto Cleanup;  
  
    //***************************************  
    pCol->dwStatus = DBSTATUS_S_OK;  
    wcscpy( (LPWSTR) pCol->bData, L"Condiments" );  
    pCol->dwLength = wcslen( (LPWSTR) pCol->bData) * sizeof(WCHAR);  
  
    /*Describe the consumer buffer by filling in the array.   
    of DBBINDING structures.  Each binding associates  
    a single parameter to the consumer's buffer.*/  
    acDBBinding[0].iOrdinal     = 1;  
    acDBBinding[0].obLength     = offsetof( COLUMNDATA, dwLength );  
    acDBBinding[0].obStatus     = offsetof( COLUMNDATA, dwStatus );  
    acDBBinding[0].pTypeInfo    = NULL;  
    acDBBinding[0].pObject      = NULL;  
    acDBBinding[0].pBindExt     = NULL;  
    acDBBinding[0].dwPart       = DBPART_VALUE | DBPART_STATUS | DBPART_LENGTH;  
    acDBBinding[0].dwMemOwner   = DBMEMOWNER_CLIENTOWNED;  
    acDBBinding[0].dwFlags      = 0;  
    acDBBinding[0].bScale       = 0;  
    acDBBinding[0].obValue      = offsetof( COLUMNDATA, bData );  
    acDBBinding[0].eParamIO     = DBPARAMIO_INPUT;  
    acDBBinding[0].cbMaxLen     = 50;   
    acDBBinding[0].wType        = DBTYPE_WSTR;  
    acDBBinding[0].bPrecision   = 0;  
  
    rgParamOrdinals[0]              = 1;  
    rgParamBindInfo[0].bPrecision   = 0;  
    rgParamBindInfo[0].bScale       = 0;  
    rgParamBindInfo[0].dwFlags      = DBPARAMFLAGS_ISINPUT;  
    rgParamBindInfo[0].pwszDataSourceType = (WCHAR *)wszDataSourceType;  
    rgParamBindInfo[0].pwszName     = (WCHAR *)wszParamName;  
    rgParamBindInfo[0].ulParamSize  = 35;  
  
    if (FAILED(hr = pICommandStream->QueryInterface(  
                        IID_ICommandWithParameters,  
                        (LPVOID *)&pICommandWithParameters)))  
    {  
        cout << "Error.\n";  
        goto Cleanup;  
    }  
  
    if (FAILED(hr = pICommandWithParameters->SetParameterInfo(  
                        nParams,  
                        rgParamOrdinals,  
                        rgParamBindInfo)))  
    {  
        cout << "Error.\n";  
        goto Cleanup;  
    }  
  
    //Create an accessor from the above set of bindings.  
    if (FAILED(hr = pICommandStream->QueryInterface(  
                                    IID_IAccessor,   
                                    (void**)&pIAccessor)))  
    {  
        cout << "Failed to get IAccessor interface.\n";  
        goto Cleanup;  
    }  
  
    if (FAILED(hr = pIAccessor->CreateAccessor(  
                            DBACCESSOR_PARAMETERDATA,  
                            nParams,   
                            acDBBinding,   
                            sizeof(SPROCPARAMS),   
                            &hAccessor,  
                            acDBBindStatus)))  
    {  
        cout << "Failed to create accessor for the defined parameters.\n";  
        goto Cleanup;  
    }  
    /*  
    Fill in DBPARAMS structure for the command execution. This structure  
    specifies the parameter values in the command and is then passed   
    to Execute.  
    */  
    params.pData = sprocparams; //pCol->bData; //sprocparams;  
    params.cParamSets = 1;  
    params.hAccessor = hAccessor;  
  
    pParams = &params;  
  
    //***************************************  
    //Execute the command.  
    if(FAILED(hr = pICommand->Execute(NULL,   
                                    IID_ISequentialStream,   
                                    pParams,   
                                    NULL,   
                                    (IUnknown **) &pStreamOutput )))  
    {  
        cout << "Failed to execute command.\n";  
        goto Cleanup;  
    }  
  
    //Process the result set.  
    if (FAILED(hr = ProcessResultSet(pStreamOutput)))  
    {  
        goto Cleanup;  
    }  
  
Cleanup:  
    //Free up memory.  
    if( pStreamOutput )  
        pStreamOutput->Release();  
    if (pICommandStream)  
        pICommandStream->Release();  
    if (pICommand)  
        pICommand->Release();  
    if (pIDBCreateCommand)  
        pIDBCreateCommand->Release();  
    if (pIDBCreateSession)  
        pIDBCreateSession->Release();  
    if (pIDBInitialize)  
        pIDBInitialize->Release();  
  
    if (hr)  
    {  
        IErrorInfo* pErrorInfo = NULL;  
        BSTR        bstrDesc = NULL;  
        GetErrorInfo(0, &pErrorInfo);  
        if (pErrorInfo)  
        {  
            pErrorInfo->GetDescription(&bstrDesc);  
            printf ("\r\nError: %S\r\n", bstrDesc ? bstrDesc : L"Unknown error");  
            SysFreeString(bstrDesc);  
            pErrorInfo->Release();  
        }  
    }  
  
    //Release the COM library.  
    CoUninitialize();  
};  
  
//--------------------------------------------------------------------  
HRESULT InitializeAndEstablishConnection(IDBInitialize ** ppIDBInitialize)  
{  
    HRESULT         hr = S_OK;  
    IDBInitialize * pIDBInitialize = NULL;  
    IDBProperties * pIDBProperties = NULL;  
    DBPROP          rgIDBProps[4];  
    DBPROPSET       rgIDBPropSet[1];  
    int             ii;  
  
    if (!ppIDBInitialize)  
        return E_INVALIDARG;  
  
    *ppIDBInitialize = NULL;  
  
    /*  
    Initialize the property values needed   
    to establish the connection.  
    */  
    for(ii = 0; ii < 4; ii++)   
        VariantInit(&rgIDBProps[ii].vValue);  
  
    //Obtain access to the SQLOLEDB provider.  
    if(FAILED(hr = CoCreateInstance(CLSID_SQLOLEDB,   
                          NULL,   
                          CLSCTX_INPROC_SERVER,  
                          IID_IDBInitialize,   
                          (void **) &pIDBInitialize)))  
    {  
        printf("Failed to get IDBInitialize interface.\n");  
        goto Cleanup;  
    }  
  
    //Server name.  
    rgIDBProps[0].dwPropertyID  = DBPROP_INIT_DATASOURCE;  
    rgIDBProps[0].vValue.vt     = VT_BSTR;  
    rgIDBProps[0].vValue.bstrVal= SysAllocString(L"server");  
    rgIDBProps[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgIDBProps[0].colid         = DB_NULLID;  
  
//Database.  
    rgIDBProps[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
    rgIDBProps[1].vValue.vt     = VT_BSTR;  
    rgIDBProps[1].vValue.bstrVal= SysAllocString(L"Northwind");  
    rgIDBProps[1].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgIDBProps[1].colid         = DB_NULLID;  
  
//User name (login).  
    rgIDBProps[2].dwPropertyID  = DBPROP_AUTH_USERID;   
    rgIDBProps[2].vValue.vt     = VT_BSTR;  
    rgIDBProps[2].vValue.bstrVal= SysAllocString(L"sa");  
    rgIDBProps[2].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgIDBProps[2].colid         = DB_NULLID;  
  
//Password.  
//    rgIDBProps[3].dwPropertyID  = DBPROP_AUTH_PASSWORD;   
//    rgIDBProps[3].vValue.vt     = VT_BSTR;  
//    rgIDBProps[3].vValue.bstrVal= SysAllocString(L"password");  
//    rgIDBProps[3].dwOptions     = DBPROPOPTIONS_REQUIRED;  
//    rgIDBProps[3].colid         = DB_NULLID;  
  
    /*  
    Now that the properties are set, construct the DBPROPSET structure  
    (rgInitPropSet). The DBPROPSET structure is used to pass an array   
    of DBPROP structures (rgIDBProps) to the SetProperties method.  
    */  
    rgIDBPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
//  rgInitPropSet[0].cProperties    = 4;  
    rgIDBPropSet[0].cProperties    = 3;  
    rgIDBPropSet[0].rgProperties   = rgIDBProps;  
  
    //Set initialization properties.  
    if (FAILED(hr = pIDBInitialize->QueryInterface(IID_IDBProperties,   
                                   (void **)&pIDBProperties)))  
    {  
        cout << "Failed to get IDBProperties interface.\n";  
        goto Cleanup;  
    }  
  
    if (FAILED(hr = pIDBProperties->SetProperties(1, rgIDBPropSet)))  
    {  
        cout << "Failed to set initialization properties.\n";  
        goto Cleanup;  
    } //end if  
  
    //Now establish the connection to the data source.  
    if(FAILED(hr = pIDBInitialize->Initialize()))  
    {  
        cout << "Problem in establishing connection to the data source.\n";  
        goto Cleanup;  
    }  
  
    *ppIDBInitialize = pIDBInitialize;  
  
Cleanup:  
    for(ii = 0; ii < 4; ii++)   
        VariantClear(&rgIDBProps[ii].vValue);  
  
    if (pIDBProperties)  
        pIDBProperties->Release();  
    return hr;  
} //End of InitializeAndEstablishConnection.  
  
HRESULT SetCommandProperties(ICommand * pICommand)  
{  
    HRESULT     hr = S_OK;  
    DBPROP      rgProps[1];  
    DBPROPSET   rgPropSet[1];  
    ICommandProperties* pICommandProperties = NULL;  
  
    VariantInit(&rgProps[0].vValue);  
  
    //Server name.  
    rgProps[0].dwPropertyID  = SSPROP_STREAM_BASEPATH;  
    rgProps[0].vValue.vt     = VT_BSTR;  
    rgProps[0].vValue.bstrVal= SysAllocString(L"D:\\Test");  
    rgProps[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgProps[0].colid         = DB_NULLID;  
  
    /*  
    Now that the properties are set, construct the DBPROPSET structure  
    (rgInitPropSet). The DBPROPSET structure is used to pass an array   
    of DBPROP structures (rgProps) to the SetProperties method.  
    */  
    rgPropSet[0].guidPropertySet = DBPROPSET_SQLSERVERSTREAM;  
    rgPropSet[0].cProperties    = 1;  
    rgPropSet[0].rgProperties   = rgProps;  
  
    // Get an ICommandProperties interface.  
    if(FAILED(pICommand->QueryInterface( IID_ICommandProperties, (void**) &pICommandProperties)))  
    {  
        cout << "Failed to get an ICommandProperties interface.\n";  
        goto Cleanup;  
    }  
  
    //Set initialization properties.  
    if(FAILED(hr = pICommandProperties->SetProperties(1, rgPropSet)))  
    {  
        cout << "Failed to set command properties.\n";  
        goto Cleanup;  
    }  
Cleanup:  
    VariantClear(&rgProps[0].vValue);  
    if (pICommandProperties)  
        pICommandProperties->Release();  
    return hr;  
}  
  
//--------------------------------------------------------------------  
//Retrieve and display data resulting from a query.  
HRESULT ProcessResultSet(ISequentialStream * pStreamOutput)  
{  
    CHAR    szBuf[1000];  
    ULONG   ulNumRead;  
    HRESULT hr;  
  
    if( pStreamOutput == NULL )  
        return E_INVALIDARG;  
  
    // Read from the stream  
    ZeroMemory( szBuf, 1000 );  
    while( ( hr = pStreamOutput->Read( szBuf, 1000, &ulNumRead ) ) == S_OK )  
    {  
        cout << szBuf;  
        cout.flush();  
    }  
    return hr;  
} //ProcessResultSet.  
```  
  
  
