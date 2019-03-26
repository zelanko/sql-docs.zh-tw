---
title: catalog.create_environment_variable (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 91ed017b-6567-4bf2-b9f1-e2b5c70a5343
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 10460dc01d07e9fe73a4f9e320d262311e9018a3
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58272595"
---
# <a name="catalogcreateenvironmentvariable-ssisdb-database"></a>catalog.create_environment_variable (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中建立環境變數。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.create_environment_variable [@folder_name =] folder_name  
    , [@environment_name =] environment_name  
    , [@variable_name =] variable_name  
    , [@data_type =] data_type  
    , [@sensitive =] sensitive  
    , [@value =] value  
    , [@description =] description  
```  
  
## <a name="arguments"></a>引數  
 [@folder_name =] *folder_name*  
 包含環境之資料夾的名稱。 *folder_name* 是 **nvarchar(128)**。  
  
 [@environment_name =] *environment_name*  
 環境的名稱。 *environment_name* 是 **nvarchar(128)**。  
  
 [@variable_name =] *variable_name*  
 環境變數的名稱。 *variable_name* 是 **nvarchar(128)**。  
  
 [@data_type =] *data_type*  
 變數的資料類型。 支援的環境變數資料類型包含 **Boolean**、**Byte**、**DateTime**、**Double**、**Int16**、**Int32**、**Int64**、**Single**、**String**、**UInt32** 和 **UInt64**。 不支援的環境變數資料類型包含 **Char**、**DBNull**、**Object** 和 **Sbyte**。 *data_type* 參數的資料類型是 **nvarchar(128)**。  
  
 [@sensitive =] *sensitive*  
 指出變數是否包含機密值。 使用 `1` 值表示環境變數的值是機密值，或者，使用 `0` 值則表示該值不是機密值。 機密值會在儲存時加密。 非機密值則會儲存為純文字。*Sensitive* 是 **bit**。  
  
 [@value =] *value*  
 環境變數的值。 *value* 是 **sql_variant**。  
  
 [@description =] *description*  
 環境變數的描述。 *value* 是 **nvarchar(1024)**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   環境的 READ 和 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   資料夾名稱、環境名稱或環境變數名稱無效  
  
-   變數名稱已經存在於環境中  
  
-   使用者未具備適當的權限  
  
## <a name="remarks"></a>Remarks  
 環境變數可以用來將值有效地指派給專案參數或封裝參數，以用於封裝的執行中。 環境變數啟用了參數值的組織。 變數名稱在環境中必須是唯一的。  
  
 預存程序會驗證變數的資料類型，以確定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄可支援該變數。  
  
> [!TIP]  
>  請考慮使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的 **Int16** 資料類型，而非使用不受支援的 **Sbyte** 資料類型。  
  
 根據下表，傳遞到這個具有 *value* 參數之預存程序的值，將會從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型：  
  
|Integration Services 資料類型|SQL Server 資料類型|  
|------------------------------------|--------------------------|  
|**布林**|**bit**|  
|**位元組**|**binary**、**varbinary**|  
|**DateTime**|**datetime**、**datetime2**、**datetimeoffset**、**smalldatetime**|  
|**Double**|精確數值：**decimal**、**numeric**；近似數值：**float**、**real**|  
|**Int16**|**smallint**|  
|**Int32**|**int**|  
|**Int64**|**bigint**|  
|**Single**|精確數值：**decimal**、**numeric**；近似數值：**float**、**real**|  
|**String**|**varchar**、**nvarchar**、**char**|  
|**UInt32**|**int** (**int** 是 **Uint32** 的最接近可用對應)。|  
|**UInt64**|**bigint** (**int** 是 **Uint64** 的最接近可用對應)。|  
  
  
