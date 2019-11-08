---
title: ProcessId 類別（SqlService）
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProcessId Class (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8418bd70e3aa2b28e0274bec63c312aba2849b84
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2019
ms.locfileid: "73657069"
---
# <a name="processid-class-sqlservice-class"></a>ProcessId 類別 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得可唯一識別服務的系統處理序識別碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ProcessId [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Uint32**值，指定可唯一識別進程的識別碼。  
  
## <a name="remarks"></a>備註  
  
## <a name="example"></a>範例  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>另請參閱  
 [啟動和停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
