---
title: SQL Server Native Client 組態屬性 (旗標索引標籤)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ab0b5bc623ef87725cd51b404eb40e158272ad76
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75306848"
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>SQL Server Native Client 組態屬性 (旗標索引標籤)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  這部電腦上的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 程式庫檔案中提供的通訊協定，來與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器通訊。 此頁面提供用戶端電腦的設定，要求使用安全通訊端層 (SSL) 來建立加密的連接。 若無法建立加密的連接，則連接會失敗。  
  
 登入過程一律加密。 下列選項只適用於加密資料。 如需有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何加密通訊的詳細資訊，以及如何設定用戶端信任伺服器憑證之根授權單位的相關指示，請參閱＜加密 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連線＞以及＜如何：啟用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的加密連接 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員)＞(位於《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中)。  
  
## <a name="options"></a>選項。  
 **強制通訊協定加密**  
 使用 SSL 來要求連接。  
  
 **信任伺服器憑證**  
 當設定為 **[否]** 時，用戶端處理序會嘗試驗證伺服器憑證。 用戶端和伺服器各需擁有公開憑證授權單位所發行的憑證。 若用戶端電腦沒有憑證，或憑證驗證失敗，則會結束連接。  
  
 當設定為 **[是]** 時，用戶端不會驗證伺服器憑證，因此會啟用自我簽署憑證。  
  
 只有在 **[強制通訊協定加密]** 設定為 **[是]** 時，才能使用 **[信任伺服器憑證]** 。  
  
  
