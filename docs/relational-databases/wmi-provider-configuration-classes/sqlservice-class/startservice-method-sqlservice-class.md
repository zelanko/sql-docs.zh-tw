---
title: StartService 方法 （SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StartService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartService method
ms.assetid: 83dfb6bd-dbd5-45d8-aad2-a11926317f91
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4589eac1a564ee06f96d175eda8dcf63d860a262
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51668157"
---
# <a name="startservice-method-sqlservice-class"></a>StartService 方法 (SqlService 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  嘗試將此服務置於它的啟動狀態。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.StartService()  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定下列其中一個啟動狀態的 uint32 值。  
  
 0  
 成功。 要求已被接受。  
  
 1  
 不支援。 不支援此要求。  
  
 2  
 拒絕存取。 使用者沒有適當的存取權限。  
  
 3  
 相依的服務正在執行中。 無法停止此服務，因為與它相依的其他服務正在執行中。  
  
 4  
 服務控制無效。 要求的控制碼無效，或是服務不接受此控制碼。  
  
 5  
 服務無法接受控制。 服務 (Win32_BaseService:State) 的狀態等於 0、1 或 2，因此無法將要求的控制碼傳送至服務。  
  
 6  
 服務不在使用中。 尚未啟動服務。  
  
 7  
 服務要求逾時。 服務並未及時回應啟動要求。  
  
 8  
 未知的失敗。 啟動服務時發生未知的失敗。  
  
 9  
 找不到路徑。 找不到通往服務可執行檔的目錄路徑。  
  
 10  
 服務已經在執行中。 服務已在執行中。  
  
 11  
 服務資料庫已鎖定。 要加入新服務的資料庫已被鎖定。  
  
 12  
 服務相依性已刪除。 已經從系統中移除這個服務所依賴的相依性。  
  
 13  
 服務相依性失敗。 服務在相依的服務中找不到所需的服務。  
  
 14  
 服務已停用。 已經從系統中停用服務。  
  
 15  
 服務登入失敗。 此服務未通過驗證，無法在系統上執行。  
  
 16  
 服務已標示為要刪除。 正在從系統中移除此服務。  
  
 17  
 服務沒有執行緒。 服務沒有執行緒。  
  
 18  
 狀態循環相依性。 啟動服務時有循環的相依性。  
  
 19  
 狀態重複名稱。 有一個服務在相同名稱下執行。  
  
 20  
 狀態名稱無效。 服務名稱中有無效的字元。  
  
 21  
 狀態參數無效。 已經將無效的參數傳遞給服務。  
  
 22  
 狀態服務帳戶無效。 執行此服務所使用的帳戶無效，或是它缺少執行此服務的權限。  
  
 23  
 狀態服務存在。 服務存在於系統可使用之服務的資料庫中。  
  
 24  
 服務已經暫停。 服務目前在系統中暫停。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
