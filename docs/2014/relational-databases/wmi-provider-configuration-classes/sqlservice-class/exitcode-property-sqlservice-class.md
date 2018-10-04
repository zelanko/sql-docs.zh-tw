---
title: ExitCode 屬性 （SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- ExitCode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6852086b6e65857284f7c5ee37e550b11d66839f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48064828"
---
# <a name="exitcode-property-sqlservice-class"></a>ExitCode 屬性 (SqlService 類別)
  取得或設定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 錯誤碼，該錯誤碼會定義啟動和停止服務時所遇到的問題。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.ExitCode [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定結束碼的 `uint32` 值。  
  
## <a name="remarks"></a>備註  
 當錯誤對於此類別所代表的服務而言是唯一時，此屬性會設定為 ERROR_SERVICE_SPECIFIC_ERROR (1066)。 服務執行時會將此值設定為 NO_ERROR，並在正常結束後再將此值設定為 NO_ERROR。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
