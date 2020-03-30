---
title: SQL Server 備份應用程式 - 磁碟區陰影複製服務 (VSS) 和 SQL 寫入器
description: 描述 SQL 寫入器元件及其在 SQL Server 資料庫的 VSS 快照集建立和還原程序中所扮演的角色。
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c62a2dfb1a6728098c3faeed32ce842dbab4304e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "77146730"
---
# <a name="sql-server-back-up-applications---volume-shadow-copy-service-vss-and-sql-writer"></a>SQL Server 備份應用程式 - 磁碟區陰影複製服務 (VSS) 和 SQL 寫入器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 會藉由提供寫入器 (SQL 寫入器) 來支援磁碟區陰影複製服務 (VSS)，讓協力廠商備份應用程式可以使用 VSS 架構來備份資料庫檔案。 本文件描述 SQL 寫入器元件及其在 SQL Server 資料庫的 VSS 快照集建立和還原程序中所扮演的角色。 其中也會詳細說明如何設定及使用 SQL 寫入器，以搭配 VSS 架構中的備份應用程式運作。


## <a name="introduction"></a>簡介

SQL Server 提供支援，讓您可以使用磁碟區陰影複製服務 (VSS) 從 SQL Server 資料建立快照集。 這會藉由提供 VSS 相容寫入器 (SQL 寫入器) 來達成，讓協力廠商備份應用程式可以使用 VSS 架構來備份資料庫檔案。 本文件描述 SQL 寫入器元件及其在 SQL Server 資料庫的 VSS 快照集建立和還原程序中所扮演角色。 其中也會詳細說明如何設定及使用 SQL 寫入器，以搭配 VSS 架構內容中的備份應用程式運作。

## <a name="definition-of-terms"></a>詞彙定義

- **虛擬裝置介面**：SQL Server 提供一種稱為「虛擬裝置介面 (VDI)」的應用程式開發介面，可藉由提供備份和還原作業支援來協助獨立軟體廠商將 SQL Server 整合到其產品中。 這些 API 可提供最高的可靠性與效能，並能支援所有的 SQL Server 備份和還原功能，包括所有熱備份與快照集備份能力。 如需詳細資訊，請參閱 [SQL Server 2005 虛擬備份裝置介面規格](https://www.microsoft.com/download/details.aspx?id=17282) (英文)。 

- **要求者**：要求為一或多個原始磁碟區建立一或多個快照集的程序 (自動或 GUI)。 在本文件中，要求者也用來表示建立 SQL Server 資料庫快照集的備份應用程式。

## <a name="about-vss"></a>關於 VSS

VSS 提供在 Windows 系統上執行 VSS 應用程式的系統基礎結構。 雖然對於使用者和開發人員而言大部分是透明的，但 VSS 會執行下列作業：

- 在建立和使用陰影複製時，協調提供者、寫入器和要求者的活動。
- 提供預設系統提供者。
- 實作任何提供者運作所需的低階驅動程式功能。

VSS 服務會視需要啟動；因此，若要讓 VSS 作業成功，必須啟用此服務。

## <a name="vss-components"></a>VSS 元件

VSS 會協調下列合作元件的活動： 

- 提供者會擁有陰影複製資料並具現化陰影複製。
- 寫入器是變更資料並參與陰影複製同步處理程序的應用程式。
- 要求者會起始陰影複製的建立和解構。 我們的設計主要針對要求者是備份應用程式。

VSS 提供下列各方之間的協調： 

![協調](media/sql-server-vss-writer-backup-guide/coordinations.png)

此圖表顯示參與一般 VSS 快照集活動的所有元件。 在此案例中，SQL Server (包括 SQL 寫入器) 會作為寫入器方塊中的其中一個寫入器。  其他這類寫入器可能是 Exchange Server 等。

本文件其餘部分假設讀者已熟悉 VSS 架構的詞彙。  如需詳細資料，請參閱[磁碟區陰影複製服務](/windows/win32/vss/volume-shadow-copy-service-overview)的相關文件。

## <a name="about-sql-writer"></a>關於 SQL 寫入器

SQL 寫入器是 SQL Server 所提供的 VSS 寫入器。 其處理與 SQL Server 的 VSS 互動。 SQL 寫入器是以獨立服務形式隨附於 SQL Server，並在 SQL Server 安裝過程中一併安裝。 預設不會啟用 SQL 寫入器。 必須明確予以啟用，才能在伺服器電腦上執行。

SQL 寫入器在 VSS 快照集備份作業中的角色： 

![VSS 快照集](media/sql-server-vss-writer-backup-guide/sql-vss-snapshot.png)



## <a name="configuring-the-sql-writer"></a>設定 SQL 寫入器

SQL 寫入器服務會在 SQL Server 安裝過程中一併安裝於系統，並設定為在 Windows 啟動時自動啟動。 

### <a name="sql-writer-service-account"></a>SQL 寫入器服務帳戶

在安裝期間，會安裝 SQL 寫入器帳戶以使用本機系統帳戶。 由於 SQL 寫入器需要使用專屬的 VDI API 來與 SQL Server 通訊，因此 SQL 寫入器帳戶必須具有足夠的 SQL Server 和 VSS 存取權限。  將此服務設定為本機系統帳戶會提供足夠的權限，讓服務正常執行。

  > [!NOTE]
  > 若要讓 SQL 寫入器服務正常運作，請務必確定本機系統帳戶未從 SQL Server 執行個體的 'SA' 角色中移除。

### <a name="enabling-and-starting-sql-writer"></a>啟用和啟動 SQL 寫入器

若要啟動和使用 SQL 寫入器，必須完成下列作業：

您可以將 SQL 寫入器服務設為 [自動] 來啟用此服務。 若要透過控制台開啟服務，請依序按一下 [開始] 和 [控制台]，然後依序按兩下 [系統管理工具] 和 [服務]。 在 [服務] 窗格中，按兩下 SQL 寫入器服務，然後將 [啟動類型] 屬性修改為 [自動]。

在上述服務屬性畫面中，選取 [服務狀態] 屬性下的 [啟動] 按鈕，也應該會啟動服務。

為了方便起見，SQL 寫入器服務會在第一次啟動時自動進行這些變更。

  > [!NOTE]
  > 在 SQL Server Express 執行個體已安裝，且有應用程式正在使用 [使用者執行個體] 功能的特定情況下，SQL Server 可能會自動啟動 SQL 寫入器。 這麼做是為了在 VSS 備份作業期間，協助列舉這些使用者執行個體。 

## <a name="backuprestore-operations-and-supported-versions"></a>備份/還原作業和支援的版本

### <a name="version-support"></a>版本支援

SQL 寫入器隨附於 SQL Server，且僅支援 SQL Server 執行個體。 

此外，SQL 寫入器還會列舉 SQL Server Express 執行個體。 SQL 寫入器也會列舉由 SQL Server Express 啟動的使用者執行個體。


## <a name="supported-backuprestore-operations"></a>支援的備份/還原作業

SQL Server (使用 SQL 寫入器) 將支援下列以 VSS 為基礎的備份作業模式：

- 以非元件為基礎
- 以元件為基礎

### <a name="noncomponent-based-backup-operations"></a>以非元件為基礎的備份作業

以非元件為基礎的備份使用快照集中磁碟區清單來隱含選取資料庫。 SQL 寫入器會檢查是否有損毀資料庫，並在找到時引發錯誤。 損毀資料庫是磁碟區清單在其中選取檔案子集的資料庫。

在以非元件為基礎的模型中，僅支援簡單復原模式的資料庫。 不支援在還原後向前復原。

### <a name="component-based-backup-operations"></a>以元件為基礎的備份作業

SQL 寫入器偏好且建議使用以元件為基礎的備份，因為應用程式 (VSS 備份應用程式) 會從 SQL 寫入器傳回的中繼資料明確選取資料庫。 快照集應該包含備份這些資料庫所需的所有磁碟區。 VSS 基礎結構不會自動新增所選資料庫集所需的磁碟區。 所有備份磁碟區都應該包含在磁碟區快照集中。 備份應用程式會負責確保所有備份磁碟區都包含在快照集中。  SQL 寫入器會偵測損毀資料庫 (其備份磁碟區在快照集外)，並使備份失敗。

本主題其餘部分假設會在 SQL Server 的 VSS 快照集建立過程中，使用以元件為基礎的備份。

## <a name="features-supported-by-sql-writer"></a>SQL 寫入器支援的功能


- **全文檢索**：SQL 寫入器會報告寫入器中繼資料文件中資料庫元件下具有遞迴檔案規格的全文檢索目錄容器。  選取資料庫元件時會自動包含在備份中
- **差異備份/還原**：SQL 寫入器透過兩種 VSS 差異機制來支援差異備份/還原：部分檔案，以及依上次修改時間的差異檔案。
- **部分檔案**： SQL 寫入器使用 VSS 部分檔案機制，以報告其資料庫檔案內已變更的位元組範圍。  
- **依上次修改時間的差異檔案**：SQL 寫入器使用 VSS 依上次修改時間的差異檔案機制，以報告全文檢索目錄中已變更的檔案。
- **以移動的方式還原**：SQL 寫入器在還原期間支援 VSS 的新目標規格。  VSS 的新目標規格允許將資料庫/記錄檔或全文檢索目錄容器重新定位為部分還原作業。
- **重新命名資料庫**：要求者可能需要使用新的名稱來還原 SQL 資料庫，特別是當資料庫與原始資料庫並存還原時。 只要資料庫保留在原始 SQL 執行個體中，SQL 寫入器就支援在還原作業期間重新命名資料庫。
- **只複製備份**：您有時必須建立適用於特殊目的備份，例如當需要建立資料庫複本來進行測試時。  此備份不應該影響資料庫的整體備份和還原程序。 使用 COPY_ONLY 選項指定備份在「頻外」完成，且不應該影響正常的備份順序。 SQL 寫入器支援 SQL Server 執行個體的「只複製」備份類型。
- **自動復原資料庫快照集**： 一般而言，使用 VSS 架構取得的 SQL Server 資料庫快照集會處於非復原狀態。 在資料集中的資料通過復原階段之前，您無法安全地存取資料，以回復進行中的交易並將資料庫置於一致狀態。 VSS 備份應用程式可以在快照集建立過程中要求自動復原快照集。

如需這些新功能及其用法的更詳細描述，請參閱本主題中的＜備份與還原選項詳細資料＞。

### <a name="what-is-not-supported"></a>不支援的功能

- SQL 寫入器不支援記錄備份。
- 不支援檔案/檔案群組備份。
- 不支援分頁還原。
- 不支援資料庫快照集，且會在同時建立元件和非元件 VSS 快照集時予以忽略。 
- 自動關閉資料庫，或已啟用關機的資料庫。
- Linux 不提供 VSS 架構，因此無法在 Linux 上使用 SQL 寫入器

下表列出 SQL 寫入器/SQL Server 針對所有 SQL Server 版本使用 VSS 架構所支援的快照集備份類型。

| **備份/還原作業**                 | **以元件為基礎**           | **以非元件為基礎** |
|:-------------------------------------------- | :---------------------------- | :--------------------- |
|完整資料備份 </br> (包括全文檢索目錄)| 是                     | 是                    |
|完整還原                                  | 是                           | 是                    |
|完整還原 (不復原)                    | 是                           | 否                     |
|差異備份                           | 是                           | 否                     |
|差異還原                          | 是                           | 否                     |
|以移動的方式還原                             | 是                           | 否                     |
|重新命名資料庫                               | 是                           | 否                     |
|只複製備份                              | 是                           | 否                     |
|自動復原的快照集                       | 是                           | 否                     |
|記錄備份                                    | 否                            | 否                     |
|資料庫快照集                            | 否                            | 否                     |
|自動關閉資料庫</br> 已啟用關機的資料庫 | 是                        | 否                     |
|可用性群組資料庫                  | 是                           | 在次要上為否        | 




## <a name="snapshot-creation-process"></a>快照集建立程序

VSS 架構會在 SQL Server 快照集建立期間，協調要求者 (備份應用程式 ) 和 SQL 寫入器的活動。 為了啟用此協調，VSS 架構會定義要求者和寫入器介面。  參與的要求者應用程式和寫入器都應該實作這些介面。 SQL 寫入器會實作必要的寫入器介面。 在快照集建立過程中，VSS 架構會呼叫 SQL 寫入器的介面。 SQL 寫入器會與系統上的 SQL Server 執行個體互動，以協助建立快照集。

VSS 架構會定義一組可供要求者/備份應用程式使用的 API。 備份應用程式開發人員必須遵循這些 API 呼叫模式，才能利用 VSS 架構快照集建立程序。 下一節將從 SQL 寫入器的觀點來描述快照集建立程序。 其中也會詳細說明要求者、VSS 架構、SQL 寫入器和 SQL Server 執行個體之間的一些內部互動。 如需這些步驟的詳細資訊，以及 VSS 架構介面的詳細資料，請參閱磁碟區陰影複製服務的相關文件。    

  > [!NOTE]
  > 假設讀者已大致熟悉 VSS 架構和備份建立程序。 這些章節可作為補充資訊，說明 SQL 寫入器如何參與 VSS 備份建立程序。

## <a name="snapshot-creation-workflow"></a>快照集建立工作流程

![資料流程](media/sql-server-vss-writer-backup-guide/dataflow-chart.png)

上圖顯示以元件為基礎其快照集建立/備份作業期間的資料流程圖。 為了更充分了解執行備份所牽涉到的基本工作，將此概觀細分成下列階段會很有用：

- 備份初始化
- 備份探索階段
- 備份前工作
- 實際檔案備份
- 備份終止



### <a name="backup-initialization"></a>備份初始化

在此備份階段期間，要求者 (備份應用程式) 會繫結至快照集介面 **IvssBackupComponents**，並將其初始化以準備備份。 它也會呼叫 VSS API **IVssGatherWriterMetadata**，以指示 VSS 架構從所有寫入器收集中繼資料。

VSS 架構會使用 **OnIdentify** 事件來呼叫每個註冊的寫入器 (包括 SQL 寫入器)，以取得寫入器中繼資料。 SQL 寫入器會查詢 SQL Server 執行個體，以取得每個資料庫的備份中繼資料資訊，並建立寫入器中繼資料文件。 此階段也稱為「中繼資料列舉」。

寫入器中繼資料文件是包含從寫入器傳送到要求者 (備份應用程式) 的資訊文件。 寫入器中繼資料文件包含下列資訊：

- 應用程式識別碼和易記名稱。
- 檔案和元件存在的位置。
- 備份中必須包含和排除的檔案。
- 還原時應該使用的選項。
- 這會透過 VSS 架構傳回給要求者。

### <a name="sql-writer-metadata-document"></a>SQL 寫入器中繼資料文件

這是寫入器 (在此案例中為 SQL 寫入器) 使用 **IVssCreateWriterMetadata** 介面所建立的 XML 文件，其中會包含寫入器狀態和元件的資訊。 如需寫入器中繼資料文件的結構詳細資料描述，請參閱 VSS API 文件。 以下是 SQL 寫入器中繼資料文件的部分詳細資料。

- 寫入器識別資訊
    - **寫入器名稱** - L"SqlServerWriter"
    - **寫入器類別識別碼** - 0xa65faa63、0x5ea8、0x4ebc、0x9d、0xbd、0xa0、0xc4、0xdb、0x26、0x91、0x2a 
    - **寫入器執行個體識別碼** - L"SQL Server:SQLWriter" 
    - **VSSUsageType** - VSS_UT_USERDATA 
    - **VSSSourceType** - VSS_ST_TRANSACTEDDB 
- 寫入器層級資訊 - VSS_APP_BACK_END 
- 還原方法規格 - VSS_RME_RESTORE_IF_CAN_REPLACE。
- 支援的備份架構 (IVssCreateWriterMetadata::SetBackupSchema API)
    - VSS_BS_DIFFERENTIAL - 差異備份
    - VSS_BS_TIMESTAMPED - 以時間戳記為基底 - 適用於全文檢索目錄檔案。
    - VSS_BS_LAST_MODIFY - 根據上次修改時間的差異備份。
    - VSS_BS_WRITER_SUPPORTS_NEW_TARGET - 支援新目標位置選項。
    - VSS_BS_WRITER_SUPPORTS_RESTORE_WITH_MOVE - 支援「以移動的方式」還原
    - VSS_BS_COPY - 支援「只複製」備份選項。
- 元件層級資訊：這包含 SQL 寫入器所提供的元件層級特定資訊。
   - **類型** - VSS_CT_FILEGROUP
   - **名稱** - 元件的名稱 (資料庫名稱)
   - **邏輯路徑** - 伺服器執行個體的邏輯路徑 (具名執行個體的格式為 "server\instance-name"，預設執行個體為 "server")。
   - **元件旗標**
   - **VSS_CF_APP_ROLLBACK_RECOVERY** - 表示 SQL Server 快照集一律需要「復原」階段，才能讓檔案一致並可用於非備份 (也就是應用程式回復) 案例。
   - Selectable - True
   - SelectableForRestore - True 
   - 支援的還原方法 - VSS_RME_RESTORE_IF_CAN_REPLACE

SQL Server 中元件集結構的唯一延伸模組是引進全文檢索目錄。  全文檢索目錄是容器目錄，無法以 VSS 資料庫或記錄檔表示，因為 VSS 資料庫和記錄檔沒有遞迴規格。  因此，SQL 寫入器會使用 VSS 檔案群組元件 (VSS_CT_FILEGROUP) 來表示資料庫層級元件，並使用檔案群組檔案來表示資料庫、記錄和全文檢索目錄檔案。

本文件結尾會提供寫入器中繼資料文件範例。

### <a name="backup-discovery"></a>備份探索
在此階段中，要求者會檢查寫入器中繼資料文件，然後建立**備份元件文件**並填入每個需要備份的元件。 它也會指定所需備份選項和參數來作為此文件的一部分。 針對 SQL 寫入器，每個需要備份的資料庫執行個體都是個別元件。

#### <a name="backup-components-document"></a>備份元件文件
這是要求者在設定還原或備份作業的過程中所建立的 XML 文件 (使用 **IVssBackupComponents** 介面)。 備份元件文件包含從參與備份或還原作業的一或多個寫入器明確加入的元件清單。 不包含隱含加入的元件資訊。 相反地，寫入器中繼資料文件只會包含可能參與備份的寫入器元件。 如需備份元件文件的結構詳細資料描述，請參閱 VSS API 文件。

#### <a name="prebackup-tasks"></a>備份前工作
VSS 下的備份前工作著重於建立包含備份資料的磁碟區陰影複製。 備份應用程式會儲存來自陰影複製的資料，而不是實際磁碟區。

要求者通常會在準備備份期間及建立陰影複製時等候寫入器。 如果 SQL 寫入器參與備份作業，則必須設定其檔案及本身以準備備份和陰影複製。

#### <a name="prepare-for-backup"></a>準備備份
要求者必須設定需要執行的備份作業類型 (**IVssBackupComponents::SetBackupState**)，然後透過 VSS 通知寫入器以使用 **IVssBackupComponents::PrepareForBackup** 準備備份作業。

SQL 寫入器會取得備份元件文件的存取權，其中詳細說明需要備份的資料庫。 所有備份磁碟區都應該包含在磁碟區快照集中。 SQL 寫入器會偵測損毀資料庫 (其備份磁碟區在快照集外)，並在 PostSnapshot 事件期間使備份失敗。

**起始快照集**：要求者會藉由呼叫 VSS 架構介面 DoSnapshotSet 來起始快照集程序。

**建立快照集**：此階段牽涉到 VSS 架構與 SQL 寫入器之間的一連串互動。

1. _準備快照集_： SQL 寫入器會呼叫 SQL Server 來準備建立快照集。
1. _凍結_：SQL 寫入器會針對每個要在快照集中備份的資料庫，呼叫 SQL Server 來凍結所有資料庫 I/O。 一旦凍結事件回到 VSS 架構，VSS 就會建立快照集。
1. _解除凍結_： 發生此事件時，SQL 寫入器會呼叫 SQL Server 執行個體來「解除凍結」或恢復正常的 I/O 作業。


快照集建立階段的速度很快 (不到 60 秒)，因此可避免封鎖資料庫的所有寫入。

**快照後**：如果快照集需要自動復原，SQL 寫入器會針對每個已選取要在快照集中的資料庫執行自動復原。 如需詳細說明，請參閱＜自動復原的快照集＞。

#### <a name="actual-backup-of-files"></a>實際檔案備份

在此階段中，要求者可以視需要將資料移至備份媒體。 此階段中的互動是在要求者與 VSS 架構之間進行。 不會牽涉到 SQL 寫入器。

1. 取得寫入器狀態。 傳回寫入器的狀態。 要求者可能需要處理此處的任何失敗。
1. 執行備份。

此時，要求者可以視需要將資料移至備份媒體。

#### <a name="backup-complete"></a>備份完成

此事件會指出備份已成功完成。

如果目前的備份是資料庫的完整備份 (而不是只複製備份)，SQL 寫入器也可以在此時將備份認可為差異基底。


  > [!NOTE]
  > 要求者應該明確地傳送此事件 (「備份完成」事件)，以允許 SQL 寫入器認可差異基底備份。 如果未收到此事件，則建立的備份將不會是合格的「差異基底」備份。

#### <a name="save-writer-metadata"></a>儲存寫入器中繼資料

要求者應該儲存備份元件文件和每個元件備份中繼資料，以及從快照集備份的資料。 SQL 寫入器/SQL Server 需要這些寫入器中繼資料，才能進行還原作業。

#### <a name="backup-termination"></a>備份終止

要求者會藉由釋放 **IVssBackupComponents** 介面或呼叫 **IVssBackupComponents::DeleteSnapshots** 來終止陰影複製。

## <a name="restore-process"></a>還原程序

本節描述還原作業工作流程及各個相關步驟。

### <a name="restore-operation-workflow"></a>還原作業工作流程

下圖顯示 VSS 還原作業期間的資料流程圖。 為了更充分了解執行還原所牽涉到的基本工作，將此概觀細分成下列主題會很有用：

- 還原初始化
- 準備還原
- 實際檔案還原
- 還原清除和終止

![還原程序流程](media/sql-server-vss-writer-backup-guide/restore-process-flow.png)

在所有以元件為基礎的 VSS 還原案例中，SQL 寫入器會分兩個不同階段來處理資料庫還原。

- **還原前**：SQL 寫入器會處理驗證、關閉檔案控制代碼等。
- **還原後**：SQL 寫入器會附加資料庫，並視需要執行損毀復原。

在這兩個階段之間，備份應用程式會負責在 SQL 底下四處移動相關資料。

### <a name="restore-initialization"></a>還原初始化

在還原的初始化階段期間，要求者必須能夠存取儲存的備份元件文件。

在備份作業期間所產生備份元件文件會當作備份資料的一部分來儲存。 備份應用程式必須將此資料傳回 VSS 架構。 SQL 寫入器會在還原程序一開始取得此資料的存取權。

#### <a name="prepare-for-restore"></a>準備還原

準備還原時，要求者會使用已儲存備份元件文件來判斷要還原的內容和方法。  要求者會選取要還原的元件，並視需要設定適當的還原選項。

如果備份應用程式想要在目前的還原作業上套用差異或記錄備份 (例如需要「使用 norecovery 還原」)，則應該在為每個要還原的資料庫建立元件過程中設定下列選項。

```
IVssBackupComponents::SetAdditionalRestores(true)
```

在備份元件文件中設定所有必要的詳細資料之後，要求者會進行 **IVssBackupComponents::PreRestore** 呼叫，透過 VSS 產生 PreRestore 事件，以供寫入器處理。

SQL 寫入器會檢查提供的備份元件文件，以識別適當的資料庫，並刪除自備份後所建立的任何其他檔案。 它也會檢查磁碟空間，並關閉任何開啟的資料庫檔案控制代碼，讓要求者可以在還原階段期間複製所需的資料。 此階段可在要求者執行實際檔案複製之前，及早偵測到任何錯誤狀況。 SQL Server 也會將資料庫置於正在還原狀態。  從此刻起到成功還原為止，都無法啟動資料庫。

#### <a name="restore-files"></a>還原檔案

這純粹是要求者特定的動作。 要求者 (備份應用程式) 會負責將所需資料庫檔案 (或要進行差異還原的相關資料範圍) 複製到適當的位置。 此作業不會牽涉到 SQL 寫入器。

#### <a name="cleanup-and-termination"></a>清除和終止

將所有資料還原到正確的位置之後，要求者會進行呼叫以通知還原作業已完成 (**IvssBackupComponents::PostRestore**)，讓 SQL 寫入器知道可以開始執行還原後動作。  此時，SQL 寫入器會執行損毀復原的重做階段。 如果未要求復原 (也就是要求者未指定 SetAdditionalRestores(true))，則在此階段期間，也會執行復原步驟的恢復階段。

## <a name="backup-and-restore-option-details"></a>備份與還原選項詳細資料

本節詳細描述 SQL 寫入器支援的所有備份與還原選項。

### <a name="requestor-creates-a-volume-shadow-copy"></a>要求者建立磁碟區陰影複製

磁碟區陰影複製建立程序 (在備份/還原內容外) 可能牽涉到 SQL 寫入器，因為已將資料庫檔案的備份磁碟區新增至磁碟區快照集。  在此情況下，SQL 寫入器只會參與中繼資料列舉、凍結、解除凍結、PrepareForSnapshot 和 PostSnapshot 協調 (如需詳細資料，請參閱資料流程圖)。

### <a name="full-backuprestore"></a>完整備份/還原

SQL 寫入器支援在以非元件和以元件為基礎的模式中進行完整備份/還原作業。

### <a name="noncomponent-based-backup-and-restore"></a>以非元件為基礎的備份與還原

在以非元件為基礎的備份/還原中，要求者會指定要備份/還原的磁碟區或資料夾樹狀目錄。 這會備份/還原指定磁碟區/資料夾中的所有資料。

#### <a name="backup"></a>Backup

在以非元件為基礎的備份中，SQL 寫入器會藉由使用快照集中的磁碟區清單來隱含選取資料庫。  寫入器會檢查是否有損毀資料庫，並在找到時引發錯誤。 損毀資料庫是磁碟區清單在其中選取檔案子集的資料庫。  不支援透過 SQL 寫入器在還原後向前復原 (差異或記錄還原)。

#### <a name="restore"></a>還原

要求者會還原在以非元件為基礎的模式中所備份資料庫。  您無法在這類還原之後執行向前復原的還原，例如記錄還原或差異還原。

針對以非元件為基礎的還原作業，必須對離線 SQL Server 執行個體或已捨棄/中斷連結的目標資料庫執行還原，以確保檔案離線。  這會就地複製檔案，並接著附加資料庫。 全部都會在 SQL 寫入器的範圍外進行。

### <a name="component-based-backup-and-restore"></a>以元件為基礎的備份與還原

在以元件為基礎的備份中，要求者會明確選取要備份/還原的資料庫元件 (從 SQL 寫入器傳回給用戶端的中繼資料)。

#### <a name="backup"></a>Backup

在以元件為基礎的備份中，所選資料庫的所有備份磁碟區都應該包含在磁碟區快照集中。  否則，SQL 寫入器會偵測損毀資料庫 (其備份磁碟區在快照集外)，並使備份失敗。  完整備份會備份資料庫資料和所有必要的記錄檔，以便在還原時將資料庫回復成交易一致狀態。

#### <a name="full-restore-without-rollforward"></a>不需要進行向前復原的完整還原

資料庫備份其完整還原有時會在不需要額外進行任何向前復原的情況下完成。 這可能是由於沒有可協助向前復原的中繼資料所致，或在某些情況下，不需要向前復原。 本節簡短說明這兩種情況。  

#### <a name="no-metadatano-rollforward"></a>沒有中繼資料/不向前復原

如果在備份作業期間不會儲存寫入器中繼資料 (以元件為基礎的備份中繼資料)，則必須對離線 SQL Server 執行個體或已捨棄/中斷連結的目標資料庫執行還原，以確保檔案離線。  這會就地複製檔案，並接著附加資料庫。 全部都會在 SQL 寫入器的範圍外進行。

#### <a name="metadata-exist-but-no-additional-rollforward-is-needed"></a>中繼資料存在，但不需要額外進行向前復原

要求者會還原在以元件為基礎的模式中所備份資料庫，但不會要求向前復原。 在此情況下，SQL Server 會在還原過程中對資料庫執行損毀復原。

**額外進行向前復原的完整還原**：要求者可以指定 SetAdditionalRestores(true) 選項來發出還原。  此選項表示要求者將接著進行更多向前復原的還原 (例如記錄還原、差異還原等)。 這會指示 SQL Server 不要在還原作業結束時執行復原步驟。

這僅適用於寫入器中繼資料已在備份期間儲存，且可在還原時供 SQL 寫入器使用的情況。 SQL Server 服務必須正在執行，要求者才能指示 VSS 執行還原活動。

SQL 寫入器預期會依下列順序執行：

1. 準備還原每個資料庫。 此活動牽涉到關閉所有檔案控制代碼，以允許要求者應用程式複製/掛接資料庫檔案。
1. 要求者應用程式複製/掛接檔案。
1. 完成還原 (使用 NORECOVERY)。  資料庫已上線，但處於「正在還原」狀態。

然後可以使用傳統 SQL 備份、差異或記錄，透過 VDI/T-SQL 或藉由使用 VSS 架構套用差異還原來向前復原資料庫。

### <a name="full-text-support"></a>全文檢索支援

SQL 寫入器會報告寫入器中繼資料文件中資料庫元件下具有遞迴檔案規格的全文檢索目錄容器。  選取資料庫元件時會自動包含在備份中

### <a name="differential-backuprestore"></a>差異備份/還原

差異備份作業只會備份自最近基底完整備份後已變更的資料。 差異備份只會包含資料庫檔案的已變更部分。 若要執行這類備份，備份應用程式或要求者需要資料庫檔案中變更位置的資訊，以便備份檔案的適當區段。 在差異備份作業期間，SQL 寫入器會以「VSS 部分檔案資訊」指定的格式來提供這項資訊。 這項資訊只能用來備份資料庫檔案的已變更部分。

### <a name="backup"></a>Backup

當使用 VSS 起始備份作業時，要求者可以藉由在備份元件文件 (**IVssBackupComponents::SetBackupState**) 中設定 DIFFERENTIAL 選項 (**VSS_BT_DIFFERENTIAL**) 來發出差異備份。  SQL 寫入器會將部分檔案資訊 (由 SQL Server 傳回) 傳遞至 VSS。  要求者可以藉由呼叫 VSS API (**IVssComponent::GetPartialFile**) 來取得此檔案資訊。 此部分檔案資訊可讓要求者只選擇已變更的位元組範圍來備份資料庫檔案。

在「備份前工作」階段期間，SQL 寫入器會確保每個選取的資料庫都有單一差異基底。

在 PostSnapshot 事件期間，SQL 寫入器會從 SQL Server 取得部分檔案資訊，並使用 **IVssComponent::AddPartialFile** 呼叫，將其新增至備份元件文件。  

  > [!NOTE]
  > SQL 寫入器僅支援對差異備份使用單一差異基準。 不支援多基準。

### <a name="partial-file-information-format"></a>部分檔案資訊格式

針對在差異備份期間備份的每個資料庫，SQL 寫入器會儲存每個資料庫檔案的部分檔案資訊。 要求者或備份應用程式會在實際檔案備份期間使用這項資訊，只將檔案的相關部分複製到備份媒體。 如需此部分檔案資訊格式的詳細資訊，請參閱磁碟區陰影複製服務的相關文件。

要求者可以藉由呼叫 **IVssComponent::GetPartialFileCount** 和 **IVssComponent::GetPartialFile** 來判斷這些檔案。  **IVssComponent::GetPartialFile** 會傳回指向檔案的路徑和檔案名稱，以及指出在檔案中所需要備份內容的範圍字串。

如需部分檔案資訊擷取的詳細資訊，請參閱 [VSS 文件](/windows/win32/vss/volume-shadow-copy-service-overview)。

### <a name="back-up-files"></a>備份檔案

在此階段期間，備份應用程式應該會查看儲存在備份元件文件中的寫入器中繼資料，並只備份檔案的相關部分。 (針對全文檢索目錄檔案，此備份應該根據檔案時間戳記來完成。 本文件稍後會加以描述)。

差異備份一律會與資料庫現有的最新基底備份有關。  還原時，SQL Server 會偵測不相符的基底和差異備份。 因此，備份應用程式或系統管理員會負責確保差異與預期的完整備份有關。  如果某個頻外程序已建立另一個完整備份，則備份應用程式可能會由於未「擁有」基底備份，而無法還原差異。

目前，如果位元組範圍資訊 (部分檔案資訊) 太大 (超過 64 K 位元組的緩衝區大小)，則 SQL Server 將會擲回錯誤，其指示使用者執行完整備份。

### <a name="interesting-cases-during-backup"></a>備份期間的相關案例

檔案新增/捨棄/壓縮/成長/邏輯重新命名/實體重新命名是備份中的相關案例。

**取得基底之後新增的檔案**

這些檔案會包含在部分規格中，因為 SQL 資料庫檔案的每個標頭都必須在部分規格中。  除了標頭頁面之外，所有配置的頁面都必須包含在部分規格中。

**取得基底之後捨棄的檔案**

取得基底之後，可以捨棄資料檔案。  在差異備份期間，這類檔案不會包含在寫入器中繼資料文件中。  此外，也不會有與已捨棄檔案建立關聯的部分資訊。

**取得基底之後壓縮的檔案**

在伺服器中停用檔案壓縮之前，不會從檔案收集部分資訊。  這可確保永遠不會包含對應至資料檔案壓縮區域的任何部分資訊。  

**取得基底之後成長的檔案**

如果成長發生在收集部分資訊之前，則部分資訊應該包含成長區域中已配置的頁面。  如果成長發生在收集部分資訊之後，則部分資訊不會包含成長區域中的變更。  在下列各節中，我們會看到記錄向前復原將還原這類變更。

**取得基底之後邏輯重新命名的檔案**

邏輯重新命名檔案不會影響備份或還原，因為在寫入器中繼資料文件或備份元件文件中任何位置都不會參考檔案的邏輯名稱  (如需詳細資料，請參閱＜寫入器中繼資料文件：範例＞)。

**取得基底之後實體重新命名的檔案**

實體資料庫檔案重新命名會等到資料庫重新啟動才會生效。  因此，部分資訊緩衝區中的資料庫組態資訊或檔案路徑資訊仍然是以舊實體路徑為基礎，這是快照集上這些資料庫檔案的唯一有效路徑。

### <a name="restore"></a>還原

在差異還原期間，要求者傳回給 SQL 寫入器的備份中繼資料具有備份類型資訊。  因此，SQL 寫入器不需要進行特殊處理。  SQL Server 會自行判斷這是差異還原。  SQL Server 處理這類差異還原的方式，會與不透過 VSS 執行的原生差異還原相同。

### <a name="prerestore-phase"></a>還原前階段

在此階段期間，SQL Server 會根據差異備份的檔案中繼資料，將所有檔案調整為適當的大小。  如果檔案已成長，則 SQL Server 會將成長部分歸零。  如果必須建立新的檔案 (在取得基底之後建立)，則 SQL Server 會將新的檔案歸零。 它也會關閉所有的檔案控制代碼，讓備份應用程式可以使用來自備份媒體的還原資料以覆寫檔案。

### <a name="restore-files"></a>還原檔案

用戶端應該根據部分檔案規格來還原檔案。  資料應該還原到資料庫檔案的相同位移/範圍，如儲存在寫入器中繼資料中的部分檔案規格所指定。

資料庫檔案新增/捨棄/成長/壓縮/邏輯重新命名/實體重新命名同樣是還原時的相關案例。

**如果在取得完整基底之後已新增資料庫檔案**

SQL Server 必須已在還原準備階段期間預先建立這類檔案。  這類檔案應該已擴充到正確的大小，並已歸零。用戶端只需要根據部分規格來配置資料 (部分規格包含所有配置的範圍)。

**如果在取得完整基底之後已捨棄資料庫檔案**

SQL Server 所提供部分資訊不包含這類已捨棄檔案的任何追蹤資訊。  SQL Server 會負責偵測要刪除的檔案，方法是比較已還原的檔案中繼資料與現有的容器，並實際予以刪除。  這會在還原前的準備步驟中完成。

**如果在取得完整基底之後資料庫檔案已成長**

SQL Server 必須已在還原準備階段期間將這類檔案擴充到正確的大小。  SQL Server 也必須已將擴充的區域歸零。  因此，即使在成長區域中，用戶端也可以安全地根據部分規格來配置資料。  如果檔案在取得部分資訊之後成長，則會重新執行與差異備份一起備份的記錄，以還原成長區域中的變更。

**如果在取得完整基底之後資料庫檔案已壓縮**

SQL Server 會負責根據中繼資料，將檔案截斷成所需的大小。  這會在還原前的準備步驟中完成。

**如果在取得完整基底之後已邏輯重新命名資料庫檔案**

這不會影響還原，因為邏輯名稱不會出現在寫入器中繼資料文件或備份元件文件中。  當用戶端將變更套用至主要資料庫檔案 (其中包含系統目錄資訊) 時，將會還原邏輯名稱變更。

**如果在取得完整基底之後已實體重新命名資料庫檔案。**

如果在差異備份時，重新命名尚未生效，則用戶端仍然會將資料還原到舊的位置。  還原後重新啟動資料庫將會使實體重新命名生效。  如果在差異備份時，實體檔案重新命名已生效，則會從新的實體路徑備份部分資料 (如果有的話)。  

### <a name="post-restore"></a>還原後

在還原後事件期間，SQL 寫入器會執行資料庫的一般重做作業和復原 (如果 SetAdditionalRestores() 設定為 False)。

## <a name="differential-backuprestore-for-full-text-catalogs"></a>全文檢索目錄的差異備份/還原

SQL Server 全文檢索目錄是資料庫資源的一部分，其必須與資料庫檔案的其餘部分一起備份或還原。  差異備份是以全文檢索目錄的時間戳記為基底。  SQL Server VSS 差異備份/還原具有單一基底備份。  換句話說，不同容器不會有不同的基底。  對於 VSS 全文檢索目錄備份而言，這表示針對所有全文檢索目錄容器，差異備份會以單一時間戳記為基底；不同於原生 SQL 差異備份案例，其中每個全文檢索目錄容器各有一個時間戳記基底。

在 VSS 中，此時間戳記會以完整備份期間所設定的全元件屬性表示，並在後續的差異備份期間使用。  

### <a name="onidentify"></a>OnIdentify

在 OnIdentify 中，SQL 寫入器會呼叫 IVssCreateWriterMetadata::SetBackupSchema() 來設定 VSS_BS_TIMESTAMPED 值。  這會向備份應用程式指出 SQL 寫入器負責管理差異基底。

### <a name="setting-the-base-timestamp"></a>設定基底時間戳記

基底時間戳記是在完整備份期間所設定。  在 **OnPostSnapshot()** 中，寫入器會叫用 **IVssComponent::SetBackupStamp()** ，將時間戳記與元件一起儲存在備份文件中。

### <a name="differential-backup"></a>差異備份

備份應用程式會從基底完整備份擷取此時間戳記，並呼叫 **IVssComponent::GetBackupStamp()** 將時間戳記提供給寫入器，以從先前的基底備份擷取基底戳記。  然後，它會呼叫 **IVssBackupComponent::SetPreviousBackupStamp()** 將其提供給寫入器。  寫入器會接著呼叫 **IVssComponent::GetPreviousBackupStamp()** 來擷取戳記，並將其轉譯為用於 **IVssComponent::AddDifferencedFilesByLastModifyTime()** 的時間戳記。  

**備份應用程式在差異備份期間的職責**：在差異備份期間，備份應用程式會負責：

- 備份其上次修改時間戳記大於元件中所設定檔案「上次修改時間」指定時間戳記的任何檔案 (整個檔案)。
- 追蹤和偵測已刪除的檔案。  

**備份應用程式在差異還原期間的職責**：在差異還原期間，備份應用程式會負責：

- 藉由建立新檔案 (如果檔案不存在) 或覆寫現有檔案 (如果檔案已存在) 來還原已備份的所有檔案。
- 如果還原檔案大於現有檔案，請先擴充檔案，再配置內容。
- 如果還原檔案小於現有檔案，請將檔案截斷成與還原檔案相同的大小。
- 刪除所有應該刪除的檔案，也就是那些不應該在差異備份時存在的檔案。

### <a name="copy-only-backup"></a>只複製備份

您有時必須建立適用於特殊目的的備份。 例如，您可能需要建立資料庫複本來進行測試。  此備份不應該影響資料庫的整體備份和還原程序。 使用 COPY_ONLY 選項指定備份在「頻外」完成，且不應該影響正常的備份順序。 SQL 寫入器支援 SQL Server 執行個體的「只複製」備份類型。

在備份探索階段期間，SQL 寫入器會藉由使用 **IVssCreateWriterMetadata::SetBackupSchema** 呼叫設定支援的備份架構選項 VSS_BS_COPY，以表示其能夠執行只複製備份。 要求者可以將備份類型設定為只複製備份，方法是使用呼叫 **IVssBackupComponents::SetBackupState**，將 VSS_BACKUP_TYPE 選項設定為 VSS_BT_COPY。

選取只複製備份時，會假設磁碟上的檔案將複製到備份媒體 (由要求者)，而不論每個檔案的備份記錄狀態為何。 SQL Server 不會更新備份記錄。 這類備份不會構成進一步差異備份作業的基底備份，也不會干擾先前差異備份的記錄。

### <a name="restore-with-move"></a>以移動的方式還原

VSS 允許備份應用程式 (要求者) 使用 **IVssComponent::SetNewTarget** 呼叫來指定新的還原目標。  在 PreRestore() 和 PostRestore() 中，SQL 寫入器會檢查是否已指定至少一個新目標。 備份應用程式會負責在實際檔案還原/複製期間，將檔案實體複製到新的位置。

備份應用程式只能指定新的實體路徑目標，不能指定檔案規格。  例如，針對位於 c:\data\test.mdf 的資料庫檔案，無法變更實際檔案名稱 test.mdf。  只能變更路徑 c:\data。  針對位於 c:\ftdata\foo 的全文檢索目錄容器，由於 VSS 中的檔案規格是 "*"，而 VSS 中的路徑規格是 c:\ftdata\foo，因此可以變更整個路徑。  

### <a name="database-rename"></a>重新命名資料庫

要求者可能需要使用新的名稱來還原 SQL 資料庫，特別是當資料庫與原始資料庫並存還原時。  要求者可以在還原作業期間指定此選項，方法是使用 VSS 呼叫 **IVssBackupComponents::SetRestoreOptions()** (在 wszRestoreOptions 參數中)，將自訂還原選項設定為「新元件名稱」= <「新名稱」>。

SQL 寫入器會取得 [新元件名稱] 值的完整內容，並用作還原資料庫的新名稱。 如果未指定任何選項，SQL 會使用資料庫的原始名稱 (元件名稱) 來還原資料庫。

  > [!NOTE]
  > SQL 寫入器目前不支援「跨執行個體重新命名」，以將資料庫移至新的執行個體。

### <a name="auto-recovered-snapshots"></a>自動復原的快照集

一般而言，使用 VSS 架構取得的 SQL Server 資料庫快照集會處於非復原狀態。 在資料集中的資料通過復原階段之前，您無法安全地存取資料，以回復進行中的交易並將資料庫置於一致狀態。 由於快照集處於唯讀狀態，因此無法藉由附加資料庫的一般程序來復原。

您可以在快照集建立過程中自動復原快照集。 在寫入器中繼資料文件中，SQL 寫入器會指定元件旗標 "VSS_CF_APP_ROLLBACK_RECOVERY"，以指出當指定快照集時，必須先對快照集上的資料庫執行復原，才能存取資料庫。要求者可以指出快照集應該是應用程式回復快照集 (也就是說，快照集中的所有資料庫檔案都必須處於一致的應用程式使用狀態)，還是備份快照集 (用於備份資料以在稍後系統失敗時進行還原的快照集)。

要求者應該設定 VSS_VOLSNAP_ATTR_ROLLBACK_RECOVERY，以指出此元件是針對非備份目的而進行備份。  VSS 接著會將 SQL 寫入器在所選元件上指定的 VSS_CF_APP_ROLLBACK_RECOVERY 與 VSS_VOLSNAP_ATTR_ROLLBACK_RECOVERY 相互關聯，並判斷是否會發生自動復原。  VSS 會讓快照集在有限時間內可供寫入，並自動將 VSS_VOLSNAP_ATTR_AUTORECOVERY 位元新增至快照集內容。

若為 SQL Server，自動復原應該只會套用至應用程式回復快照集，而不會套用至備份快照集。 針對應用程式回復快照集，SQL 寫入器會在 PostSnapShotevent 期間起始自動復原程序。 此程序會對要求者在快照集中明確選取的每個 SQL Server 資料庫執行下列動作：

- 將快照集資料庫附加至原始 SQL Server 執行個體 (也就是原始資料庫所附加的執行個體)。
- 復原資料庫 (這會在「附加」作業過程中發生)。
- 壓縮記錄檔。

    如果 VSS 提供者是「軟體提供者」，這可減少需要由 VSS 架構完成的不必要「寫入時複製」量。 壓縮記錄檔是預設行為。 這可以透過將下列登錄機碼值設定為 1 來停用。
    
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SQLWriter\
    Settings\DisableLogShrink
    
    若是為了修正線上資料庫問題，而可能使用快照集從記錄的特定頁面 (在特定時間點) 匯出資料，在此情況下可能會很有用。

- 卸離資料庫。

現在我們有了一致性復原快照集，可附加用於查詢。

### <a name="multi-database-transactions"></a>多資料庫交易

在某些情況下，資料庫快照集可能會包含一些進行中的多資料庫交易。 在復原作業期間，SQL 寫入器會使用 presume abort 選項在快照集上附加資料庫。 這會回復尚未認可的任何多資料庫交易 (包括處於 [準備認可] 狀態的任何交易)。 這可能會導致快照集中資料庫之間出現一些不一致的情況。 例如，假設有兩個資料庫 A 和 B。這兩個資料庫之間有分散式交易，而此交易在資料庫 A 中處於 [已認可] 狀態，在資料庫 B 中則處於 [準備認可] 狀態。在自動復原過程中，此交易會在資料庫 A 中認可，並在資料庫 B 中回復。這可能會導致快照集中出現一些不一致的情況。

VSS 架構在 Longhorn 時間範圍內發行的 Microsoft Distributed Transaction Coordinator (MS DTC) 元件，將會針對跨越 SQL Server 執行個體內資料庫的交易，修正此不一致問題。 SQL Server 未來版本將會針對跨越 SQL Server 執行個體內資料庫的交易，修正這些不一致的情況。

### <a name="security-implications-for-autorecovered-snapshots"></a>自動復原快照集的安全性影響

針對 VSS 快照集，在自動復原之後，會使用存取控制清單 (ACL) 來保護檔案，只允許存取 SQL Server 帳戶所屬的特殊 Builtin 群組。  這表示任一 Box 管理員的成員或特殊群組都將能夠附加資料庫。 要求在快照集上附加資料庫檔案的用戶端，必須是 Builtin/Administrators 的成員或 SQL Server 帳戶。

### <a name="special-cases"></a>特殊案例

本節描述以 SQL 寫入器為基礎的備份與還原作業期間所遇到一些特殊案例。

#### <a name="autoclose-databases"></a>自動關閉資料庫

針對以非元件為基礎的備份，會在檢查損毀條件時完成資料庫的自動關閉，但不會在備份作業期間明確凍結自動關閉的資料庫。

這裡預期的案例是可能存在許多已關閉資料庫，而我們想要將快照集的成本降到最低。  已自動關閉資料庫通常會用於資源短缺的低階組態。

#### <a name="file-list"></a>檔案清單

在「準備備份」事件之前的列舉步驟期間，會決定每個資料庫的檔案清單。  如果資料庫檔案清單在列舉到凍結之間有所變更，除非應用程式重新檢查檔案清單，否則資料庫可能已損毀。 我們不認為這是問題，但這是廠商必須注意的事項。

#### <a name="stopped-instances"></a>已停止的執行個體

如果 SQL Server 執行個體在發生列舉步驟時不在執行中，則無法選取這些執行個體的任何資料庫。

如果執行個體在列舉到「準備備份」事件之間停止，則會忽略已停止執行個體中的任何資料庫。

#### <a name="system-and-user-databases"></a>系統和使用者資料庫

SQL Server 中的系統資料庫包括 master、model 和 msdb 資料庫，這些資料庫會隨附於 SQL Server 一併安裝。 本節描述如何在 VSS 快照集備份程序中處理這些資料庫。

### <a name="system-databases"></a>系統資料庫

Master 資料庫只能透過下列方式來還原：停止執行個體，取代資料庫檔案 (由備份應用程式完成)，然後重新啟動執行個體。 無法進行向前復原。

SQL 寫入器支援線上還原 model 和 msdb 資料庫，而不需要關閉執行個體。


#### <a name="simple-recovery-model-user-databases"></a>簡單復原模式的使用者資料庫

如果 master 資料庫與使用簡單復原模式的使用者資料庫一起還原，則可以使用與 master 資料庫相同的技術來還原使用者資料庫：在執行個體關閉的情況下，直接複製或掛接磁碟區。  啟動 SQL 執行個體時，即會復原所有內容。

#### <a name="rolling-forward-user-databases"></a>向前復原使用者資料庫

若要在復原 master 資料庫時，同時復原和向前復原使用者資料庫，則執行個體不得同時啟動和復原 master 和使用者資料庫。

此程序如下所示：

1. 確定已停止 SQL Server 執行個體。
1. 分兩階段執行還原。
    1. 經由透過 VSS 的檔案複製/磁碟區掛接，還原應該同時復原的系統資料庫和使用者資料庫 (也就是簡單復原模式的使用者資料庫)。
        1. 如果要向前復原的使用者資料庫與系統資料庫不在相同磁碟區，則此時不應該復原磁碟區。 此案例需要在備份之前進行規劃。
        1. 如果使用者資料庫與系統資料庫位於相同的磁碟區，則必須向 SQL Server 隱藏使用者資料庫。
    1. 使用 -f 參數啟動 SQL Server 執行個體  (使用 -f 啟動選項時，只能還原 master 資料庫)。
        1. 針對要向前復原的每個資料庫，發出 ALTER DATABASE \<x> SET OFFLINE  (或者中斷連結資料庫)。
        1. 停止 SQL Server 執行個體。
        1. 啟動 SQL Server 執行個體 (SQL Server 不會看到要向前復原的使用者資料庫檔案)。

使用 VSS 來還原具有 NORECOVERY 的使用者資料庫，如＜進行向前復原的完整還原＞中所述。

## <a name="appendix"></a>附錄

### <a name="writer-metadata-document--an-example"></a>寫入器中繼資料文件：範例

假設有一個名為 DB1 的範例資料庫，其屬於電腦 Server1 上的 SQL Server 執行個體 Instance1，並包含下列資料庫/記錄檔：

- 儲存在 c:\db\DB1.mdf 且名為 "primary" 的資料庫檔案
- 儲存在 c:\db\DB1.ndf 且名為 "secondary" 的資料庫檔案
- 儲存在 c:\db\DB1.ldf 且名為 "log" 的資料庫記錄檔
- 儲存在目錄 c:\db\ftdata\foo 下且名為 "foo" 的全文檢索目錄
- 儲存在目錄 c:\db\ftdata\bar 下且名為 "bar" 的全文檢索目錄。

下列為資料庫的寫入器中繼資料：

**資料庫層級檔案群組元件**

- ComponentType：VSS_CT_FILEGROUP
- LogicalPath："Server1\Instance1"
- ComponentName："DB1"
- Caption：NULL
- pbIcon：NULL
- cbIcon：0
- bRestoreMetadata：FALSE
- NotifyOnBackupComplete：TRUE
- Selectable：TRUE
- SelectableForRestore：TRUE
- ComponentFlags：VSS_CF_APP_ROLLBACK_RECOVERY

**檔案群組檔案**

- LogicalPath："Server1\Instance1"
- GroupName："DB1"
- Path："c:\db"
- FileSpec："DB1.mdf"
- Recursive：FALSE
- AlternatePath：NULL
- BackupTypeMask：VSS_FSBT_ALL_BACKUP_REQUIRED | VSS_FSBT_ALL_SNAPSHOT_REQUIRED
- 檔案群組檔案
- LogicalPath："Server1\Instance1"
- GroupName："DB1"
- Path："c:\db"
- FileSpec："DB1.ndf"
- Recursive：FALSE
- AlternatePath：NULL
- BackupTypeMask：VSS_FSBT_ALL_BACKUP_REQUIRED | VSS_FSBT_ALL_SNAPSHOT_REQUIRED

**檔案群組檔案**

- LogicalPath："Server1\Instance1"
- GroupName："DB1"
- Path："c:\db"
- FileSpec："DB1.ldf"
- Recursive：FALSE
- AlternatePath：NULL
- BackupTypeMask：VSS_FSBT_ALL_BACKUP_REQUIRED | VSS_FSBT_ALL_SNAPSHOT_REQUIRED

**檔案群組檔案：**

- LogicalPath："Server1\Instance1"
- GroupName："DB1"
- Path："c:\db\ftdata\foo"
- FileSpec："*"
- Recursive：TRUE
- AlternatePath：NULL
- BackupTypeMask：VSS_FSBT_ALL_BACKUP_REQUIRED | VSS_FSBT_ALL_SNAPSHOT_REQUIRED

**檔案群組檔案：**

- LogicalPath："Server1\Instance1"
- GroupName："DB1"
- Path："c:\db\ftdata\bar"
- FileSpec："*"
- Recursive：TRUE
- AlternatePath：NULL
- BackupTypeMask：VSS_FSBT_ALL_BACKUP_REQUIRED | VSS_FSBT_ALL_SNAPSHOT_REQUIRED

如果伺服器執行個體是電腦上的預設執行個體，則邏輯路徑會變成一個部分 - "Server1"。


    
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [只複製備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)    
 [SQL Server 交易記錄架構與管理指南](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)
  
