---
title: DataReader 目的地自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 62b6f628614d533e1bebcce071ce4761e73e08f7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432195"
---
# <a name="datareader-destination-custom-properties"></a>DataReader 目的地自訂屬性
  DataReader 目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 DataReader 目的地的自訂屬性。 除了 `DataReader` 以外的所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|DataReader|String|DataReader 目的地的類別名稱。|  
|FailOnTimeout|Boolean|指出發生 `ReadTimeout` 時是否會失敗。 此屬性的預設值為 **False**。|  
|ReadTimeout|整數|發生逾時之前的毫秒數。 此屬性的預設值為 30000 (30 秒)。|  
  
 DataReader 目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [DataReader 目的地](datareader-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  
