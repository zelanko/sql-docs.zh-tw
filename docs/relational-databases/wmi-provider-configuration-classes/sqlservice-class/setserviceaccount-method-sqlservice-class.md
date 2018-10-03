---
title: SetServiceAccount 方法 （SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- SetServiceAccount Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 27985e94766a76efa755d05e81bce3ccb59ed6c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47664327"
---
# <a name="setserviceaccount-method-sqlservice-class"></a>SetServiceAccount 方法 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  嘗試變更服務執行個體執行時所使用的使用者名稱和密碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetServiceAccount(ServiceStartName , ServiceStartPassword)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
#### <a name="parameters"></a>參數  
 *ServiceStartName*  
 指定此服務執行時所使用之帳戶名稱的字串值。 根據服務類型而定，此帳戶名稱可能是 DomainName\Username 的格式。 當它執行時，將會使用兩種格式的其中一種來記錄服務處理序：  
  
-   如果帳戶屬於內建網域，可以指定 \Username。  
  
-   如果指定 NULL，則服務會以登入**LocalSystem**帳戶。  
  
 核心或系統層級的驅動程式，如*StartName*包含驅動程式的物件名稱，\FileSystem\Rdr 或 \Driver\Xns，I/O 系統用來載入裝置驅動程式。 如果指定了 NULL，將會根據類似 DWDOM\Admin 的服務名稱，使用 I/O 系統所建立的預設物件名稱來執行驅動程式。  
  
 *ServiceStartPassword*  
 指定密碼中的帳戶名稱的字串值*StartName*參數。 如果您不要變更密碼，請指定 NULL。 如果此服務沒有密碼，請指定空字串。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 A **uint32**值，則為 0，如果成功修改此服務或不支援要求，則為 1。 任何其他數字表示發生錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
