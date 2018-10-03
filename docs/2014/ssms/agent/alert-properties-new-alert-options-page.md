---
title: 警示的內容： 新的警示 （選項頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 59e5ac1f951ce897b058d224701d1a6936bfa11f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173308"
---
# <a name="alert-properties-new-alert-options-page"></a>警示屬性：新增警示 (選項頁面)
  使用此頁面即可檢視或修改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的警示選項。  
  
## <a name="options"></a>選項。  
 **電子郵件**  
 在電子郵件通知內包含事件中的錯誤文字 (如果有的話)。  
  
 **呼叫器**  
 在呼叫器通知內包含事件中的錯誤文字 (如果有的話)。  
  
 **Net Send**  
 在 Net Send 通知內包含事件中的錯誤文字 (如果有的話)。  
  
 **要傳送的其他通知訊息**  
 鍵入要包含在通知訊息中的其他文字。  
  
 **回應間隔延遲**  
 指定事件重複發生的延遲。 某些事件會在短期間內頻繁發生。 在此情況下，您可能想要知道事件是否已經發生，但不要讓每個事件都產生回應。 使用這個選項即可指定逾時。若有設定延遲，在警示回應事件之後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 再次回應之前就會等候指定的延遲，不論事件是否在延遲期間有再發生。  
  
 **Minutes**  
 指定延遲，以分鐘為單位。 若要在每一次發生事件時產生回應，請指定 0 分和 0 秒。  
  
 **秒**  
 指定延遲，以秒為單位。 若要在每一次發生事件時產生回應，請指定 0 分和 0 秒。  
  
## <a name="see-also"></a>另請參閱  
 [警示](alerts.md)  
  
  
