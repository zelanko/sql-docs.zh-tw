---
title: DataReader 目的地自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c7fb15f3dda170c866bb95840a7a3cde4c19ffa1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036165"
---
# <a name="datareader-destination-custom-properties"></a>DataReader 目的地自訂屬性
  DataReader 目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 DataReader 目的地的自訂屬性。 所有的屬性，除了`DataReader`是讀取/寫入。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|DataReader|String|DataReader 目的地的類別名稱。|  
|FailOnTimeout|布林|指出發生 `ReadTimeout` 時是否會失敗。 此屬性的預設值為 **False**。|  
|ReadTimeout|Integer|發生逾時之前的毫秒數。 此屬性的預設值為 30000 (30 秒)。|  
  
 DataReader 目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [DataReader 目的地](datareader-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  