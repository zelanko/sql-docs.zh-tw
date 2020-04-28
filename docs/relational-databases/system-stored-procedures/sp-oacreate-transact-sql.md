---
title: sp_OACreate （Transact-sql） |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2ad8059466ac520b6f9f793af7670cbd73b96b38
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68107936"
---
# <a name="sp_oacreate-transact-sql"></a>sp_OACreate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立 OLE 物件的執行個體。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>引數  
 *進程*  
 這是要建立的 OLE 物件之程式化識別碼 (ProgID)。 這個字元字串描述 OLE 物件的類別，其格式為： **'**_OLEComponent_**。**_物件_**'**  
  
 *OLEComponent*是 ole Automation 伺服器的元件名稱，而*Object*是 ole 物件的名稱。 指定的 OLE 物件必須是有效的，而且必須支援**IDispatch**介面。  
  
 例如，SQLDMO.H。SQLServer 是 SQL-DMO **SQLServer**物件的 ProgID。 SQL-DMO 的元件名稱為 SQLDMO.H、 **sqlserver**物件有效，以及**Sqlserver**物件支援**IDispatch**的（如同所有 sql-dmo 物件）。  
  
 *clsid*  
 這是要建立的 OLE 物件之類別識別碼 (CLSID)。 這個字元字串描述 OLE 物件的類別，其格式如下： **' {**_nnnnnnnn-_ nnnn-nnnn-nnnnnnnnnnnn **} '**。 指定的 OLE 物件必須是有效的，而且必須支援**IDispatch**介面。  
  
 例如，{00026BA1-0000-0000-C000-000000000046} 是 SQL-DMO **SQLServer**物件的 CLSID。  
  
 _objecttoken_ **輸出**  
 是傳回的物件 token，而且必須是**int**資料類型的本機變數。這個物件 token 會識別所建立的 OLE 物件，並用於呼叫其他 OLE Automation 預存程式。  
  
 *內容*  
 指定執行新建立之 OLE 物件的執行內容。 如果指定的話，這個值必須是下列值之一：  
  
 **1** = 僅限同進程（.DLL） OLE 伺服器。  
  
 **4** = 僅限本機（.EXE） OLE 伺服器。  
  
 **5** = 同時允許同進程和本機 OLE 伺服器  
  
 如果未指定，預設值為**5**。 這個值會當做呼叫的*dwClsCoNtext*參數傳遞至**CoCreateInstance**。  
  
 如果允許同進程 OLE 伺服器（藉由使用內容值**1**或**5** ，或未指定內容值），則可以存取所擁有的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記憶體和其他資源。 同處理序 OLE 伺服器可能會損毀 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體或資源，並造成無法預期的結果，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取違規。  
  
 當您指定內容值**4**時，本機 OLE 伺服器不會有任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資源的存取權，也不能損毀[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記憶體或資源。  
  
> [!NOTE]  
>  這個預存程序的參數是依照位置來指定，而不是名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)，這個數字是 OLE Automation 物件所傳回之 HRESULT 的整數值。  
  
 如需 HRESULT 傳回碼的詳細資訊，請參閱[OLE Automation 傳回碼和錯誤資訊](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="remarks"></a>備註  
 如果啟用 OLE automation 程式， **sp_OACreate**的呼叫會啟動 ole automation 共用執行環境。 如需啟用 OLE automation 的詳細資訊，請參閱[Ole Automation 程式伺服器設定選項](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)。  
  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式批次結束時，會自動部署所建立的 OLE 物件。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定伺服器角色的成員資格，或直接在這個預存程式上執行許可權。 `Ole Automation Procedures`必須**啟用**設定，才能使用與 OLE Automation 相關的任何系統程式。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-progid"></a>A. 使用 ProgID  
 下列範例會使用其 ProgID 來建立 sql-dmo **SQLServer**物件。  
  
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
 下列範例會使用其 CLSID 來建立 sql-dmo **SQLServer**物件。  
  
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
  
  
