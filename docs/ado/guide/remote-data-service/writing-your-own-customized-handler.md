---
description: 撰寫您自己的自訂處理常式
title: 撰寫您自己的自訂處理常式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
author: rothja
ms.author: jroth
ms.openlocfilehash: bfddb0a5cbc1691a8013528abd4c1547f29e1504
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88760068"
---
# <a name="writing-your-own-customized-handler"></a>撰寫您自己的自訂處理常式
如果您是想要使用預設 RDS 支援的 IIS 伺服器系統管理員，但對使用者要求和存取權限有更大的控制權，您可能會想要撰寫自己的處理常式。  
  
 MSDFMAP。處理常式會實 **IDataFactoryHandler** 介面。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="idatafactoryhandler-interface"></a>IDataFactoryHandler 介面  
 這個介面有兩種方法： **GetRecordset** 和 **Reconnect**。 這兩種方法都需要將 [CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md) 屬性設定為 **adUseClient**。  
  
 這兩種方法都採用在 "**Handler =**" 關鍵字中的第一個逗號後面出現的引數。 例如， `"Handler=progid,arg1,arg2;"` 會傳遞的引數字串 `"arg1,arg2"` ，且 `"Handler=progid"` 會傳遞 null 引數。  
  
## <a name="getrecordset-method"></a>GetRecordset 方法  
 這個方法會查詢資料來源，並使用提供的引數來建立新的 [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件。 **記錄集**必須以**adLockBatchOptimistic**開啟，而且不得以非同步方式開啟。  
  
### <a name="arguments"></a>引數  
 ***conn***  連接字串。  
  
 ***args***  處理常式的引數。  
  
 ***查詢***  用於進行查詢的命令文字。  
  
 ***ppRS***  應傳回 **記錄集** 的指標。  
  
## <a name="reconnect-method"></a>Reconnect 方法  
 這個方法會更新資料來源。 它會建立新的 [連接](../../reference/ado-api/connection-object-ado.md) 物件，並附加指定的 **記錄集**。  
  
### <a name="arguments"></a>引數  
 ***conn***  連接字串。  
  
 ***args***  處理常式的引數。  
  
 ***pr*** **記錄集** 物件。  
  
## <a name="msdfhdlidl"></a>msdfhdl .idl  
 這是出現在**msdfhdl .idl**檔中**IDataFactoryHandler**的介面定義。  
  
```cpp
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
 [自訂檔案連接區段](./customization-file-connect-section.md)   
 [自訂檔案記錄區段](./customization-file-logs-section.md)   
 [自訂檔案 SQL 區段](./customization-file-sql-section.md)   
 [自訂檔案 UserList 區段](./customization-file-userlist-section.md)   
 [DataFactory 自訂](./datafactory-customization.md)   
 [必要的用戶端設定](./required-client-settings.md)   
 [了解自訂檔案](./understanding-the-customization-file.md)