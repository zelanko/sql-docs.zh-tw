---
title: 在 資料庫測試助理設定重新執行，SQL Server 升級
description: 設定重新執行在資料庫測試助理
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: jroth
ms.openlocfilehash: 8efef6f081395265f641197058b7920162cdde46
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794489"
---
# <a name="configure-replay-in-database-experimentation-assistant"></a>設定重新執行在資料庫測試助理

資料庫測試助理 (DEA) 會使用 SQL Server 安裝的分散式重新執行工具來重新執行擷取的追蹤針對已升級的測試環境。 建議您這麼做才能執行完整的重新執行使用小型的追蹤檔案，以確保適當的重新執行的查詢執行的測試。

## <a name="distributed-replay-requirements"></a>分散式重新執行需求

- 額外 78%的硬碟空間，才能建立 IRF Distributed Replay controller 電腦上的檔案。
- 200 MB 或 512 MB 是理想的追蹤換用大小，用以擷取生產環境或效能的追蹤。   
- Distributed Replay controller 和用戶端機器上 CPU 和 RAM 的最低需求為 3.5 GB RAM 單一核心 CPU。
- 重新執行時間大約會 1.55 倍的擷取時間的因為一個控制器和四個的子系機器用來重新執行生產追蹤。
- 如果您使用我們 「 發行 」 版本的生產環境和效能追蹤定義檔案和效能追蹤定義會篩選出追蹤感興趣的一個資料庫時，分析顯示**效能追蹤**大小大約 15 倍**生產追蹤**大小。

## <a name="set-up-a-virtual-network-or-domain"></a>設定虛擬網路或網域

Distributed 的 Replay 會要求您使用一般機器之間的帳戶。 由於此需求，並基於安全性理由，我們建議您執行 Distributed Replay，虛擬網路上或在網域控制網路上：

- 控制器和用戶端機器的環境中建立。
- 請確定，控制器和用戶端機器可以彼此互 ping 網路上。
- 分散式重新執行用戶端電腦必須能夠連線到執行 SQL Server 的重新執行目標電腦。

## <a name="set-up-the-controller-service"></a>設定控制器服務

若要設定 controller 服務：

1. 使用 SQL Server 安裝程式，以安裝 Distributed Replay controller。 如果您略過設定 Distributed Replay controller 的 SQL Server 安裝程式精靈步驟，您可以透過組態檔中設定控制器。 在一般安裝中，組態檔位於 C:\Program Files (x86) \Microsoft SQL Server\<版本\>\Tools\DReplayController\DReplayController.config。
1. 分散式重新執行控制器記錄檔位於 C:\Program Files (x86) \Microsoft SQL Server\<版本\>\Tools\DReplayController\Log。
1. 開啟 Services.msc，並移至**SQL Server Distributed Replay Controller**服務。
1. 在服務上，以滑鼠右鍵按一下，然後選取**屬性**。 將服務帳戶設定通用控制站和用戶端電腦在網路中的帳戶。
1. 選取  **確定**以關閉**屬性**視窗。
1. 重新啟動**SQL Server Distributed Replay Controller**服務從 Services.msc。 您也可以在重新啟動服務的命令列執行下列命令：<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`
1. 如需其他組態選項，請參閱 <<c0> [ 設定 Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay)。

## <a name="configure-dcom"></a>設定 DCOM

在控制器電腦上只需要此設定。

1. 開啟 dcomcnfg.exe。
1. 依序展開**Microsoft.biztalk.deployment.deployercomponent** > **電腦** > **我的電腦** > **DCOM 設定**。
1. 底下**DCOM 設定**，以滑鼠右鍵按一下**DReplayController**，然後選取**屬性**。
1. 選取 **[安全性]** 索引標籤。
1. 底下**啟動和啟用權限**，選取**自訂**，然後選取**編輯**。
1. 新增使用者，將會啟動重新執行。 本機啟動 」 和 「 本機啟用權限授與使用者。 如果啟動或從遠端啟用的使用者方案，讓使用者遠端啟動 」 和 「 遠端啟用權限。
1. 選取 [ **[確定]** 以認可變更並返回**安全性**] 索引標籤。
1. 底下**存取權限**，選取**自訂**，然後選取**編輯**。
1. 新增使用者，將會啟動重新執行。 授與使用者的本機存取權限。 如果從遠端存取控制器服務的使用者方案，讓使用者遠端存取權限。
1. 選取 [ **[確定]** 以認可變更並返回**安全性**] 索引標籤。
1. 選取 **確定**以認可變更。
1. 重新啟動 SQL Server Distributed Replay Controller 服務，從 Services.msc。 您也可以在重新啟動服務的命令列執行下列命令：<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>設定用戶端服務

您設定用戶端服務之前，請使用網路等工具 ping 來確認控制站和用戶端電腦可以進行通訊。

1. 使用 SQL Server 安裝程式，以安裝 Distributed Replay client。
1. 開啟 Services.msc，並移至 SQL Server Distributed Replay Client 服務。
1. 在服務上，以滑鼠右鍵按一下，然後選取**屬性**。 設定服務帳戶到公用網路中的控制器和用戶端機器的帳戶。
1. 選取  **確定**以關閉**屬性**視窗。 如果您略過 SQL Server 安裝程式的精靈步驟，以設定 Distributed Replay client，您可以透過組態檔來進行設定。 在一般安裝中，組態檔位於 C:\Program Files (x86) \Microsoft SQL Server\<版本\>\Tools\DReplayClient\DReplayClient.config。
1. 請確定 DReplayClient.config 檔案包含在控制器電腦的名稱，作為其控制站進行註冊。
1.  重新啟動 SQL Server Distributed Replay Client 服務，從 Services.msc。 您也可以執行下列命令，從命令列來重新啟動服務：<br/>
    `NET STOP "SQL Server Distributed Replay Client"`<br/>
    `NET START "SQL Server Distributed Replay Client"`
1. 分散式重新執行控制器記錄檔位於 C:\Program Files (x86) \Microsoft SQL Server\<版本\>\Tools\DReplayClient\Log。 記錄檔會指出是否在用戶端可以向控制器。
1. 如果設定成功，記錄檔會顯示訊息 「 控制器上註冊 < 控制站名稱\>"。
1. 如需其他組態選項，請參閱 <<c0> [ 設定 Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay)。

## <a name="set-up-distributed-replay-administration-tools"></a>設定 Distributed Replay 管理工具

若要快速測試是否 Distributed Replay 環境中運作正常，您可以使用 Distributed Replay 管理工具。 測試組態可以是多個用戶端電腦已向控制器的環境中特別有用。 您可能需要安裝 SQL Server Management Studio (SSMS) 來取得系統管理工具。

1. 請移至 SSMS 安裝位置，然後查看 Distributed Replay 管理工具 dreplay.exe 和其相依元件。
1. 開啟命令提示字元視窗，然後執行`dreplay.exe status -f 1`。
1. 如果上述所有步驟都都成功時，主控台輸出會指出控制器可以看到其用戶端`READY`狀態。

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>設定 Distributed Replay 的遠端存取的防火牆

從遠端存取 Distributed Replay 需要開啟的網域或虛擬網路內可見的連接埠。

1. 開啟**Windows 防火牆**具有**進階安全性**。
1. 移至**輸入規則**。
1. 建立新的輸入的防火牆規則，如程式 C:\Program Files (x86) \Microsoft SQL Server\<版本\>\Tools\DReplayController\DReplayController.exe。
1. 允許網域層級存取 DReplayController.exe 要能夠從遠端與控制器服務通訊的所有連接埠。
1. 儲存規則。

## <a name="set-up-target-computers"></a>設定目標電腦

兩個重新執行，才能執行 A / B 測試或實驗。 也就是說，您可能需要兩個不同的執行個體的 SQL Server 安裝移轉案例。 

您也可以在相同電腦上安裝 SQL Server 執行個體的兩個版本。 需要注意的是確定在進行重新執行時，即完全隔離的執行個體。

每個重新執行，就必須執行下列步驟：

1. 還原資料庫的備份。
1. 提供用戶端服務帳戶的使用者可以存取 SQL Server 執行個體資料庫的權限。 不需要 SQL Server 執行個體上執行查詢的權限。
1. 開始重新執行。

## <a name="next-steps"></a>後續步驟

- 若要了解如何重新執行升級的測試環境中擷取的追蹤，請參閱[重新執行追蹤](database-experimentation-assistant-replay-trace.md)。

- 如需 19 分鐘簡介 DEA 和示範，觀看下列影片：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
