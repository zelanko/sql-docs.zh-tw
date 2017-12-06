---
title: "SQL Server Native Client 組態屬性 （旗標索引標籤） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 96cb3184afd9481f91ef9d08ad4ae112425cbaac
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>SQL Server Native Client 組態屬性 (旗標索引標籤)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在此電腦上的用戶端與通訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]伺服器使用的通訊協定中提供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端程式庫檔案。 此頁面提供用戶端電腦的設定，要求使用安全通訊端層 (SSL) 來建立加密的連接。 若無法建立加密的連接，則連接會失敗。  
  
 登入過程一律加密。 下列選項只適用於加密資料。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何加密通訊的詳細資訊，以及如何將用戶端設定為信任伺服器憑證之根授權單位的指示，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書》中的＜加密 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的連接＞以及＜如何：啟用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的加密連接 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員)＞。  
  
## <a name="options"></a>選項。  
 **強制通訊協定加密**  
 使用 SSL 來要求連接。  
  
 **信任伺服器憑證**  
 當設定為 **[否]**時，用戶端處理序會嘗試驗證伺服器憑證。 用戶端和伺服器各需擁有公開憑證授權單位所發行的憑證。 若用戶端電腦沒有憑證，或憑證驗證失敗，則會結束連接。  
  
 當設定為 **[是]**時，用戶端不會驗證伺服器憑證，因此會啟用自我簽署憑證。  
  
 只有在**[強制通訊協定加密]** 設定為 **[是]** 時，才能使用 **[信任伺服器憑證]**。  
  
  
