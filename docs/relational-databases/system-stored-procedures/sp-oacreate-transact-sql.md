---
title: sp_OACreate (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5b7a56afb2ffa11dbe4ec8937efb602c13c9599d
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2019
ms.locfileid: "65450029"
---
# <a name="spoacreate-transact-sql"></a>sp_OACreate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立 OLE 物件的執行個體。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>引數  
 *progid*  
 這是要建立的 OLE 物件之程式化識別碼 (ProgID)。 這個字元字串描述 OLE 物件的類別，且具有以下格式：**'**_OLEComponent_**。**_物件_**'**  
  
 *OLEComponent*是 OLE Automation 伺服器的元件名稱及*物件*是 OLE 物件的名稱。 指定的 OLE 物件必須有效，而且必須支援**IDispatch**介面。  
  
 比方說，是 SQLDMO。SQLServer，則 SQL-DMO 的 ProgID **SQLServer**物件。 SQL-DMO 已的元件名稱是 SQLDMO， **SQLServer**物件是否有效，而且 （例如所有 SQL-DMO 物件） **SQLServer**物件支援**IDispatch**。  
  
 *clsid*  
 這是要建立的 OLE 物件之類別識別碼 (CLSID)。 這個字元字串描述 OLE 物件的類別，且具有下列形式： **' {**_nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn_**}'**。 指定的 OLE 物件必須有效，而且必須支援**IDispatch**介面。  
  
 例如，{00026BA1-0000-0000-C000-000000000046} 是 SQL-DMO 的 CLSID **SQLServer**物件。  
  
 _objecttoken_ **輸出**  
 為傳回的物件 token，且必須使用的資料型別區域變數**int**。這個物件 token 會識別建立的 OLE 物件，並會在呼叫其他 OLE Automation 預存程序。  
  
 *context*  
 指定執行新建立之 OLE 物件的執行內容。 如果指定的話，這個值必須是下列值之一：  
  
 **1** = 僅限同處理序 (.dll) OLE 伺服器。  
  
 **4** = 本機 (.exe) OLE 伺服器。  
  
 **5** = 允許同處理序和本機 OLE 伺服器  
  
 如果未指定，預設值是**5**。 這個值被當做*dwClsContext*呼叫的參數**CoCreateInstance**。  
  
 如果允許同處理序 OLE 伺服器 (使用的內容值**1**或**5**或不指定內容值)、 其記憶體的存取權和所擁有的其他資源[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 同處理序 OLE 伺服器可能會損毀 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體或資源，並造成無法預期的結果，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取違規。  
  
 當您指定的內容值**4**，本機 OLE 伺服器並沒有任何存取權[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資源，且不能損毀[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記憶體或資源。  
  
> [!NOTE]  
>  這個預存程序的參數是依照位置來指定，而不是名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)，這個數字是 OLE Automation 物件所傳回之 HRESULT 的整數值。  
  
 如需有關 HRESULT 傳回碼的詳細資訊，請參閱 < [OLE Automation 傳回碼與錯誤資訊](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="remarks"></a>備註  
 如果已啟用 OLE automation 程序，呼叫**sp_OACreate**會啟動 OLE Automation 共用的執行環境。 如需啟用 OLE automation 的詳細資訊，請參閱[Ole Automation 程序伺服器組態選項](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)。  
  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式批次結束時，會自動部署所建立的 OLE 物件。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定伺服器角色，或直接執行這個預存程序權限。 `Ole Automation Procedures` 組態必須是**啟用**使用 OLE Automation 與相關的任何系統程序。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-progid"></a>A. 使用 ProgID  
 下列範例會建立 SQL-DMO **SQLServer**使用其 ProgID 的物件。  
  
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
 下列範例會建立 SQL-DMO **SQLServer**使用 CLSID 的物件。  
  
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
 [OLE Automation 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Ole Automation 程序伺服器組態選項](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)   
 [OLE Automation 範例指令碼](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
