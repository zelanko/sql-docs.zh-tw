---
title: "撰寫您自己的自訂處理常式 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 445f0d8d7a870ceda6cf4028b0cebe9264ed8358
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="writing-your-own-customized-handler"></a>撰寫您自己的自訂處理常式
您可能想要撰寫您自己的處理常式，您是否想要支援 RDS，預設的 IIS 伺服器系統管理員，但更充分掌控使用者的要求和存取權限。  
  
 MSDFMAP。處理常式實作**IDataFactoryHandler**介面。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="idatafactoryhandler-interface"></a>IDataFactoryHandler 介面  
 這個介面有兩種方法， **GetRecordset**和**Reconnect**。 這兩種方法需要[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。  
  
 這兩種方法可接受出現在第一個逗號後面的引數"**處理常式 =**"關鍵字。 例如，`"Handler=progid,arg1,arg2;"`將傳遞的引數字串`"arg1,arg2"`，和`"Handler=progid"`會傳遞 null 引數。  
  
## <a name="getrecordset-method"></a>GetRecordset 方法  
 這個方法會查詢資料來源並建立新[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件使用提供的引數。 **資料錄集**必須以開啟**Adlockpessimistic** ，必須以非同步方式開啟。  
  
### <a name="arguments"></a>引數  
 ***conn***連接字串。  
  
 ***引數***處理常式的引數。  
  
 ***查詢***進行查詢的命令文字。  
  
 ***ppRS***指標其中**資料錄集**應該傳回。  
  
## <a name="reconnect-method"></a>重新連線方法  
 這個方法會更新資料來源。 它會建立新[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件與附加給定**資料錄集**。  
  
### <a name="arguments"></a>引數  
 ***conn***連接字串。  
  
 ***引數***處理常式的引數。  
  
 ***Pr*** A**資料錄集**物件。  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 這是介面定義**IDataFactoryHandler** ，會出現在**msdfhdl.idl**檔案。  
  
```  
[  
  uuid(D80DE8B3-0001-11d1-91E6-00C04FBBBFB3),  
  version(1.0)  
]  
library MSDFHDL  
{  
    importlib("stdole32.tlb");  
    importlib("stdole2.tlb");  
  
    // TLib : Microsoft ActiveX Data Objects 2.0 Library  
    // {00000200-0000-0010-8000-00AA006D2EA4}  
    #ifdef IMPLIB  
    importlib("implib\\x86\\release\\ado\\msado15.dll");  
    #else  
    importlib("msado20.dll");  
    #endif  
  
    [  
      odl,  
      uuid(D80DE8B5-0001-11d1-91E6-00C04FBBBFB3),  
      version(1.0)  
    ]  
    interface IDataFactoryHandler : IUnknown  
    {  
HRESULT _stdcall GetRecordset(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] BSTR query,  
      [out, retval] _Recordset **ppRS);  
  
// DataFactory will use the ActiveConnection property  
// on the Recordset after calling Reconnect.  
   HRESULT _stdcall Reconnect(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] _Recordset *pRS);  
    };  
};  
```  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接 > 一節](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案記錄檔 > 一節](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 SQL > 一節](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList > 一節](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)



