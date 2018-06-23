---
title: ProcessId 類別 （SqlService 類別） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ProcessId Class (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0acd413899fb51d5a5670352c4638f8f5552f59a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144912"
---
# <a name="processid-class-sqlservice-class"></a>ProcessId 類別 (SqlService 類別)
  取得可唯一識別服務的系統處理序識別碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.ProcessId [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定可唯一識別處理序之識別碼的 `uint32` 值。  
  
## <a name="remarks"></a>備註  
  
## <a name="example"></a>範例  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  