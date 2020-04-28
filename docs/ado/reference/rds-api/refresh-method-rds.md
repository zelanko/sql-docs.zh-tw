---
title: Refresh 方法（RDS） |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb7cb94edab6b5422c315b71c2900662f85aa1e2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963503"
---
# <a name="refresh-method-rds"></a>Refresh 方法 (RDS)
重新查詢[連接](../../../ado/reference/rds-api/connect-property-rds.md)屬性中所指定的資料來源，並更新查詢結果。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
## <a name="remarks"></a>備註  
 您必須先設定 [[連接]](../../../ado/reference/rds-api/connect-property-rds.md)、[[伺服器](../../../ado/reference/rds-api/server-property-rds.md)] 和 [ [SQL](../../../ado/reference/rds-api/sql-property.md) ] 屬性，才能使用**Refresh**方法。 表單上與 RDS 相關聯的所有資料繫結控制項 **。DataControl**物件將會反映一組新的記錄。 已發行任何預先存在的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，並捨棄任何未儲存的變更。 **Refresh**方法會自動使第一個記錄成為目前的記錄。  
  
 當您使用資料時，最好定期呼叫**Refresh**方法。 如果您取出資料，然後將它保留在用戶端電腦上一段時間，可能會變成過期。 您所做的任何變更都可能會失敗，因為其他人可能已在您之前變更記錄並提交變更。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Refresh 方法範例（VB）](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Refresh 方法範例（VBScript）](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [通訊錄命令按鈕](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate 方法（RDS）](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh 方法（ADO）](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


