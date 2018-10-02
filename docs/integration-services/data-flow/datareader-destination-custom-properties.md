---
title: DataReader 目的地自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 67de6f79ceac48dc6e81ef9b61674fd65bd24bed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636996"
---
# <a name="datareader-destination-custom-properties"></a>DataReader 目的地自訂屬性
  DataReader 目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 DataReader 目的地的自訂屬性。 除了 **DataReader** 以外的所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|DataReader|String|DataReader 目的地的類別名稱。|  
|FailOnTimeout|布林|指出發生 **ReadTimeout** 時是否會失敗。 此屬性的預設值為 **False**。|  
|ReadTimeout|Integer|發生逾時之前的毫秒數。 此屬性的預設值為 30000 (30 秒)。|  
  
 DataReader 目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [DataReader 目的地](../../integration-services/data-flow/datareader-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
