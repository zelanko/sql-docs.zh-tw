---
description: sp_OACreate (Transact-SQL)
title: sp_OACreate (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OACreate
- sp_OACreate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OACreate
ms.assetid: eb84c0f1-26dd-48f9-9368-13ee4a30a27c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: efcdc5094183143d3f45bc5a0174c0bead5381d2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541133"
---
# <a name="sp_oacreate-transact-sql"></a>sp_OACreate (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  建立 OLE 物件的執行個體。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>引數  
 *progid*  
 這是要建立的 OLE 物件之程式化識別碼 (ProgID)。 此字元字串描述 OLE 物件的類別，格式為： **'**_OLEComponent_**。**_物件_**'**  
  
 *OLEComponent* 是 ole Automation 伺服器的元件名稱，而 *物件* 是 ole 物件的名稱。 指定的 OLE 物件必須有效，且必須支援 **IDispatch** 介面。  
  
 例如，SQLDMO.H。SQLServer 是 sql-dmo **SQLServer** 物件的 ProgID。 SQL-DMO 的元件名稱為 SQLDMO.H、 **sqlserver** 物件是有效的，而且 (像所有 sql-dmo 物件一樣) **SQLServer** 物件支援 **IDispatch**。  
  
 *Clsid*  
 這是要建立的 OLE 物件之類別識別碼 (CLSID)。 此字元字串描述 OLE 物件的類別，格式如下： **' {**_nnnnnnnn-_ nnnn-nnnn-nnnnnnnnnnnn **} '**。 指定的 OLE 物件必須有效，且必須支援 **IDispatch** 介面。  
  
 例如，{00026BA1-0000-0000-C000-000000000046} 是 sql-dmo **SQLServer** 物件的 CLSID。  
  
 _objecttoken_ **輸出**  
 這是傳回的物件標記，而且必須是資料類型 **int**的本機變數。這個物件標記會識別所建立的 OLE 物件，並用於對其他 OLE Automation 預存程式的呼叫。  
  
 *內容*  
 指定執行新建立之 OLE 物件的執行內容。 如果指定的話，這個值必須是下列值之一：  
  
 **1** = 僅限同進程 ( .DLL) OLE server。  
  
 **4** = 本機 ( .exe) 僅限 OLE 伺服器。  
  
 **5** = 同時允許同進程和本機 OLE 伺服器  
  
 如果未指定，預設值為 **5**。 此值會作為對**CoCreateInstance**呼叫的*dwClsCoNtext*參數傳遞。  
  
 如果允許使用同進程 OLE 伺服器 (使用 **1** 或 **5** 的內容值，或是未指定內容值) ，它就可以存取所擁有的記憶體和其他資源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 同處理序 OLE 伺服器可能會損毀 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體或資源，並造成無法預期的結果，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取違規。  
  
 當您指定的內容值為 **4**時，本機 OLE 伺服器沒有任何資源的存取權 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，也無法損毀 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體或資源。  
  
> [!NOTE]  
>  這個預存程序的參數是依照位置來指定，而不是名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)，這個數字是 OLE Automation 物件所傳回之 HRESULT 的整數值。  
  
 如需 HRESULT 傳回碼的詳細資訊，請參閱 [OLE Automation 傳回碼和錯誤資訊](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="remarks"></a>備註  
 如果啟用 OLE automation 程式，則 **sp_OACreate** 的呼叫會啟動 ole automation 共用執行環境。 如需啟用 OLE automation 的詳細資訊，請參閱 [Ole Automation 程式伺服器設定選項](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)。  
  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式批次結束時，會自動部署所建立的 OLE 物件。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員（sysadmin** ）固定伺服器角色中的成員資格，或直接在此預存程式上執行許可權。 `Ole Automation Procedures` 必須 **啟用** 設定，才能使用任何與 OLE Automation 相關的系統程式。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-progid"></a>A. 使用 ProgID  
 下列範例會使用其 ProgID 來建立 SQL-DMO **SQLServer** 物件。  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate 'SQLDMO.SQLServer', @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
### <a name="b-using-clsid"></a>B. 使用 CLSID  
 下列範例會使用其 CLSID 來建立 SQL-DMO **SQLServer** 物件。  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate '{00026BA1-0000-0000-C000-000000000046}',  
    @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [OLE Automation 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Ole Automation 程式伺服器設定選項](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)   
 [OLE Automation 範例指令碼](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
