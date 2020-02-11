---
title: SQL Server Native Client 設定屬性 ([旗標] 索引標籤) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bf95081d3c4657dd147e06ae54d413dd96c4c18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63028291"
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>SQL Server Native Client 組態屬性 (旗標索引標籤)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端在這部電腦上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 程式庫檔案中提供的通訊協定來與伺服器通訊。 此頁面提供用戶端電腦的設定，要求使用安全通訊端層 (SSL) 來建立加密的連接。 若無法建立加密的連接，則連接會失敗。  
  
 登入過程一律加密。 下列選項只適用於加密資料。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何加密通訊的詳細資訊，以及如何將用戶端設定為信任伺服器憑證之根授權單位的指示，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書》中的＜加密 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的連接＞以及＜如何：啟用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的加密連接 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員)＞。  
  
## <a name="options"></a>選項。  
 **強制通訊協定加密**  
 使用 SSL 來要求連接。  
  
 **信任伺服器憑證**  
 當設定為 **[否]** 時，用戶端處理序會嘗試驗證伺服器憑證。 用戶端和伺服器各需擁有公開憑證授權單位所發行的憑證。 若用戶端電腦沒有憑證，或憑證驗證失敗，則會結束連接。  
  
 當設定為 **[是]** 時，用戶端不會驗證伺服器憑證，因此會啟用自我簽署憑證。  
  
 只有在 [**強制通訊協定加密**] 設定為 **[是]** 時，才能使用 [**信任伺服器憑證**]。  
  
  
