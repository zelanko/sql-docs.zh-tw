---
title: 準備輸入追蹤資料 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: c14fd3d2-5770-47c2-a851-cc13ddbc9bf5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7af5d166ec3bc059bc2628512564d92fd4cc6cad
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63150001"
---
# <a name="prepare-the-input-trace-data"></a>準備輸入追蹤資料
  您必須先從分散式重新執行管理工具開始前置處理階段，以準備輸入追蹤資料，才能透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributed Replay 功能啟動分散式重新執行。 在前置處理階段中，分散式重新執行控制器會處理追蹤資料並產生中繼檔案：  
  
 ![分散式重新執行前置處理階段](../../database-engine/media/preprocess.gif "分散式重新執行前置處理階段")  
  
 如需前置處理階段的詳細資訊，請參閱 [SQL Server Distributed Replay](sql-server-distributed-replay.md)。  
  
> [!NOTE]  
>  輸入追蹤資料必須在相容於 Distributed Replay 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本中擷取。 輸入追蹤資料也必須相容於您要針對它重新執行追蹤資料的目標伺服器。 如需有關版本需求的詳細資訊，請參閱＜ [Distributed Replay Requirements](distributed-replay-requirements.md)＞。  
  
### <a name="to-prepare-the-input-trace-data"></a>若要準備輸入追蹤資料  
  
1.  **(選擇性) 修改前置處理組態設定**：如果您想要修改前置處理組態設定 (例如要篩選系統工作階段或設定最大閒置時間)，必須修改以 XML 為基礎的前置處理組態檔 `<PreprocessModifiers>` 的 `DReplay.exe.preprocess.config`元素。 如果您修改前置處理組態檔，我們建議您修改複本，而不是原始版本。 若要修改設定，請執行下列步驟：  
  
    1.  建立預設前置處理組態檔 `DReplay.exe.preprocess.config`的複本，並重新命名新的檔案。 預設前置處理組態檔位於管理工具的安裝資料夾。  
  
    2.  修改新組態檔中的前置處理組態設定。  
  
    3.  當起始前置處理階段 (下一步) 時，使用 *preprocess* 選項的 **config_file** 參數來指定已修改組態檔的位置。  
  
     如需前置處理組態檔的詳細資訊，請參閱 [設定 Distributed Replay](configure-distributed-replay.md)。  
  
2.  **起始前置處理階段**：若要準備輸入追蹤資料，您必須以 **preprocess** 選項執行管理工具。 如需詳細資訊，請參閱[前置處理選項 &#40;Distributed Replay 管理工具&#41;](preprocess-option-distributed-replay-administration-tool.md)。  
  
    1.  開啟 Windows 命令提示字元公用程式 (`CMD.exe`)，並瀏覽至 Distributed Replay 管理工具 (`DReplay.exe`) 的安裝位置。  
  
    2.  (選擇性) 使用 *controller* 參數 **-m**指定控制器 (如果控制器服務是在與管理工具不同的電腦上執行)。  
  
    3.  使用 *input_trace_file* 參數 **-i**，指定輸入追蹤檔案的位置和名稱。  
  
    4.  使用 *controller_working_directory* 參數 **-d**，指定控制器上應該儲存中繼檔案的位置。  
  
    5.  (選擇性) 使用 *config_file* 參數 **-c**，指定前置處理組態檔的位置。 如果已修改預設前置處理組態檔的複本，使用此參數指向新的組態檔。  
  
    6.  (選擇性) 使用 *status_interval* 參數 **-f**，指定是否要讓管理工具以不同於 30 秒的頻率顯示狀態訊息。  
  
     例如，若要在控制器服務所在的電腦上起始前置處理階段，指定追蹤檔案位於 `c:\trace1.trc`、控制器工作目錄位於 `c:\WorkingDir` ，而且以預設值 30 秒的頻率顯示狀態訊息，需要語法： `dreplay preprocess -i c:\trace1.trc -d c:\WorkingDir`  
  
3.  在前置處理階段完成之後，中繼檔案會儲存在控制器工作目錄中。 若要起始事件重新執行階段，您必須以 **replay** 選項執行管理工具。 如需詳細資訊，請參閱 [重新執行追蹤資料](replay-trace-data.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Distributed Replay Requirements](distributed-replay-requirements.md)   
 [管理工具命令列選項 &#40;Distributed Replay Utility&#41;](administration-tool-command-line-options-distributed-replay-utility.md)   
 [設定 Distributed Replay](configure-distributed-replay.md)  
  
  
