---
title: ExitCode 屬性 （SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ExitCode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1217b0f942bedf04f2bab45be41ae4f067aeb74e
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51215396"
---
# <a name="exitcode-property-sqlservice-class"></a>ExitCode 屬性 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得或設定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 錯誤碼，該錯誤碼會定義啟動和停止服務時所遇到的問題。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ExitCode [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定結束碼的 **uint32** 值。  
  
## <a name="remarks"></a>備註  
 當錯誤對於此類別所代表的服務而言是唯一時，此屬性會設定為 ERROR_SERVICE_SPECIFIC_ERROR (1066)。 服務執行時會將此值設定為 NO_ERROR，並在正常結束後再將此值設定為 NO_ERROR。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
