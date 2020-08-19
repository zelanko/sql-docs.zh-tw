---
description: 推斷的維度成員 (緩時變維度精靈)
title: 推斷的維度成員 (緩時變維度精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.inferrdim.f1
ms.assetid: 809e395f-2e10-48ff-8860-56403f130628
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4066795817035e6ac149de7fd86b2f4fb816f828
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425770"
---
# <a name="inferred-dimension-members-slowly-changing-dimension-wizard"></a>推斷的維度成員 (緩時變維度精靈)

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  使用 [推斷的維度成員]**** 對話方塊來指定使用推斷的成員之選項。 在事實資料表參考尚未載入的維度成員時，推斷的成員即已存在。 當載入推斷成員的資料時，可以更新現有的記錄而不是建立新記錄。  
  
 若要深入了解這個精靈，請參閱＜ [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **啟用推斷的成員支援**  
 如果您選擇啟用推斷的成員，就必須選取下列兩個選項的其中之一。  
  
 **所有具有變更類型的資料行皆為 Null**  
 指定是否在新推斷的成員記錄中之具有變更類型的所有資料行中，輸入 Null 值。  
  
 **使用布林資料行以指出目前記錄是否為推斷的成員**  
 指定是否使用現有的布林資料行，來指出目前記錄是否為推斷的成員。  
  
 **推斷的成員指標**  
 如果您已經選擇使用布林資料行來指出上述推斷的成員，請從清單中選取資料行。  
  
## <a name="see-also"></a>另請參閱  
 [使用緩時變維度精靈來設定輸出](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
