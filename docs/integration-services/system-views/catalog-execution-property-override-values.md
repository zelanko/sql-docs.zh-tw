---
title: catalog.execution_property_override_values | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 83cbdd6f-ddde-47bf-abde-36bd24272621
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a94fef8c3b8202503f0af4c58f1b9b732102225e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85672342"
---
# <a name="catalogexecution_property_override_values"></a>catalog.execution_property_override_values 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  顯示封裝執行期間所設定的屬性覆寫值。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|property_id|**bigint**|屬性覆寫值的唯一識別碼。|  
|execution_id|**bigint**|執行執行個體的唯一識別碼 (ID)。|  
|property_path|**nvarchar(4000)**|封裝中之屬性的路徑。|  
|property_value|**nvarchar(max)**|屬性的覆寫值。|  
|sensitive|**bit**|當值為 1 時，屬性為敏感值，而且會在儲存時加密。 當值為 0 時，屬性不是敏感值，而且會儲存為純文字。|  
  
## <a name="remarks"></a>備註  
 這個檢視會針對使用 [執行封裝] 對話方塊之 [進階] 索引標籤中的 [屬性覆寫] 區段來覆寫屬性值的每個執行，顯示一個資料列。 屬性的路徑衍生自封裝工作的 [封裝路徑]  屬性。  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   執行的執行個體之 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
