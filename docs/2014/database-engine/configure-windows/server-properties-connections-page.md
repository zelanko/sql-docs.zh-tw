---
title: 伺服器屬性 (連接頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.connections.f1
ms.assetid: 33be8ac5-12dd-4b8a-99e0-68261c219dd2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c9d58fb2a5702a2a6c3f5ac74ae970411d887b62
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62809347"
---
# <a name="server-properties-connections-page"></a>伺服器屬性 (連接頁面)
  使用此頁面來檢視或修改您的連接選項。  
  
## <a name="connections"></a>連接  
 **並行連接的最大數目 (0 = 無限制)**  
 如果設定為零以外的值，則會限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許的連接數目。  
  
> [!CAUTION]  
>  設定為較小的值，例如 1 或 2，可防止管理員連接管理伺服器；不過，專用管理連接仍可以隨時連接。  
  
## <a name="default-connection-options"></a>預設連接選項  
 **Default connection options**  
 指定預設連接選項，如下表中所述。  
  
|組態選項|描述|  
|--------------------------|-----------------|  
|**停用延遲條件約束檢查**|控制暫時的或延遲的條件約束檢查。|  
|**隱含交易**|控制陳述式執行時是否隱含地啟動交易。|  
|**資料指標在認可時關閉**|控制執行認可作業後資料指標的行為。|  
|**Ansi 警告**|控制彙總警告中的截斷與 NULL。|  
|**Ansi 填補**|控制固定長度變數的填補。|  
|**Ansi Nulls**|控制使用相等運算子時 `NULL` 的處理方式。|  
|**算術中止**|查詢執行過程中發生溢位或除以零的錯誤時終止查詢。|  
|**算術忽略**|查詢過程中發生溢位或除以零的錯誤時傳回 NULL。|  
|**引號識別碼**|評估運算式時區別單引號與雙引號。|  
|**無計數**|關閉每個陳述式結束時傳回的訊息，這些訊息會說明有多少資料列受到影響。|  
|**Ansi Null 預設開啟**|更改工作階段的行為，使 Null 屬性與 ANSI 相容。 新定義的資料行若未明確定義 Null 屬性，就允許 Null。|  
|**Ansi Null 預設關閉**|更改工作階段的行為，使 Null 屬性與 ANSI 不相容。 新定義的資料行若未明確定義 Null 屬性，就不允許 Null。|  
|**串連 Null 產生 Null**|將字串與 NULL 值串連時傳回 NULL。|  
|**數值捨入中止**|運算式中發生失去有效位數時產生錯誤。|  
|**xact 中止**|如果 Transact- SQL 陳述式引發執行階段錯誤，就回復交易。|  
  
 如需連接選項的詳細資訊，請搜尋線上叢書的特定選項。  
  
## <a name="remote-server-connections"></a>遠端伺服器連接  
 **允許此伺服器的遠端連接**  
 從遠端伺服器執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體，控制預存程序的執行。 選取這個核取方塊的效果與將 **sp_configureremote access** 選項設為 1 相同。 清除該核取方塊可避免從遠端伺服器執行預存程序。  
  
 **遠端查詢逾時 (以秒為單位，0 = 不會逾時)**  
 指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 逾時之前，遠端作業可以執行多久 (以秒為單位)。預設值是 600 秒，也就是允許等候十分鐘。  
  
 **需要伺服器對伺服器通訊的分散式交易**  
 透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 交易，保護伺服器對伺服器程序的動作。 如需詳細資訊，請參閱 [設定 remote proc trans 伺服器組態選項](configure-the-remote-proc-trans-server-configuration-option.md)。  
  
## <a name="property-page-display-options"></a>屬性頁面顯示選項  
 **設定的值**  
 針對此窗格中的選項，顯示設定的值。 如果您變更這些值，請按一下 **[執行中的值]** ，即可查看變更是否已生效。 如果沒有的話，就必須先重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
 **[執行中的值]**  
 針對此窗格中的選項，檢視目前執行中的值。 這些值是唯讀的。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;查詢執行的選項： SQL Server： Advanced Page&#41;](../options-query-execution-sql-server-advanced-page.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
