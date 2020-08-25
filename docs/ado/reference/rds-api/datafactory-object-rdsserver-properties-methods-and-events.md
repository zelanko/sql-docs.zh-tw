---
description: DataFactory 物件 (RDSServer) 屬性、方法和事件
title: DataFactory 物件 (RDSServer) 屬性、方法和事件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory object [ADO], members
ms.assetid: 36a1f49b-91f4-44f4-b6e2-52fc7ed06d7e
author: rothja
ms.author: jroth
ms.openlocfilehash: afc3b34dec0360930acdd333a97a62577ce334c8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768467"
---
# <a name="datafactory-object-rdsserver-properties-methods-and-events"></a>DataFactory 物件 (RDSServer) 屬性、方法和事件
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="properties"></a>屬性  
 無。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|-|-|  
|[ConvertToString 方法 (RDS)](./converttostring-method-rds.md)|將記錄集轉換成 MIME64 字串。|  
|[CreateRecordset 方法 (RDS)](./createrecordset-method-rds.md)|建立並傳回空的記錄集。|  
|[Execute 方法 (RDS)](./execute-method-rds.md)|執行要求，並建立 advanced data 資料列集 (，以用於 ADO 2.5 或更新版本的) 。|  
|[Execute21 方法 (RDS)](./execute21-method-rds.md)|執行要求，並建立「advanced data 資料列集」 (以用於 ADO 2.1) 。|  
|[Query 方法 (RDS)](./query-method-rds.md)|執行要求，並建立 advanced data 資料列集。|  
|[SubmitChanges 方法 (RDS)](./submitchanges-method-rds.md)|如果記錄集具有暫止的變更，這個方法就會將它們提交至連接字串中所識別的資料庫。|  
|[Synchronize 方法 (RDS)](./synchronize-method-rds.md)|將指定的記錄集與連接字串所指定的資料庫同步處理 (，以用於 ADO 2.5 或更新版本的) 。|  
|[Synchronize21 方法 (RDS)](./synchronize21-method-rds.md)|將指定的記錄集與連接字串所指定的資料庫同步處理 (以便與 ADO 2.1) 搭配使用。|  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 物件 (RDSServer)](./datafactory-object-rdsserver.md)