---
title: 新增延伸模組
description: 了解如何從 Microsoft 和協力廠商所提供的項目中選取和安裝延伸模組，將功能新增到 Azure Data Studio。
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 10/03/2019
ms.openlocfilehash: eb6578f69ab9c0ded637ef9762ea50cfd18a25bb
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411114"
---
# <a name="extend-the-functionality-of-azure-data-studio"></a>擴充 Azure Data Studio 的功能

Azure Data Studio 中的延伸模組提供一種簡單方式，讓您將更多功能新增至基底 Azure Data Studio 安裝。

延伸模組是由 Azure Data Studio 小組 (Microsoft) 及協力廠商社群 (您！) 提供。 如需建立延伸模組的詳細資訊，請參閱[延伸模組撰寫](extension-authoring.md)。

## <a name="add-azure-data-studio-extensions"></a>新增 Azure Data Studio 延伸模組

1. 透過選取 [延伸模組] 圖示或透過選取 [檢視] 功能表中的 [延伸模組]，以存取可用的延伸模組。 您可使用 [檢視：顯示延伸模組] 命令，可在 [命令選擇區] (F1 或 `Ctrl+Shift+P`) 中找到。

    ![延伸模組管理員圖示](media/extensions/extension-manager-icon.png)

    您也可以按下 `Ctrl+Shift+X` (Windows/Linux) 或 `Command+Shift+X` (Mac) 以快速存取延伸模組管理員。

2. 選取可用的延伸模組，檢視詳細資料。

    ![延伸模組詳細資料](media/extensions/extension-details.png)

3. 選取您想要的延伸模組並加以**安裝**。

4. 安裝之後，請**重新載入**以在 Azure Data Studio 中啟用延伸模組 (只有在第一次安裝延伸模組時才需要)。

若無法存取 Azure Data Studio 上的延伸模組管理員，您可以在我們的 [GitHub Wiki](https://github.com/microsoft/azuredatastudio/wiki/List-of-Extensions) \(英文\) 下載延伸模組。


## <a name="manage-extensions"></a>管理延伸模組 

### <a name="list-installed-extensions"></a>列出已安裝的延伸模組 

預設 [延伸模組] 檢視會顯示目前已啟用的延伸模組、所有建議使用的延伸模組，以及所有目前已停用延伸模組的摺疊容器。 [延伸模組：顯示已安裝的延伸模組] 命令，可在 [命令選擇區] 或 [其他動作] `(...)` 下拉式功能表中找到，此命令會顯示所有已安裝的延伸模組清單，包括已停用的延伸模組。

### <a name="uninstall-an-extension"></a>解除安裝延伸模組

若要解除安裝延伸模組，請按一下延伸模組項目右邊的齒輪圖示，然後從下拉式功能表中選擇 [解除安裝]。 此動作會解除安裝選取的延伸模組，並提示重新載入 Azure Data Studio。

 ![延伸模組下拉式清單](media/extensions/extension-gear-dropdown.png)

### <a name="disable-an-extension"></a>停用延伸模組

您可暫時停用延伸模組，而無須永久移除延伸模組。 您可停用所有 Azure Data Studio 工作階段的延伸模組 ([停用])，或僅針對目前的工作區 ([停用 (工作區)])。 您也可以在 [命令選擇區] 中停用所有目前已安裝的延伸模組，只要使用 [延伸模組：停用所有延伸模組] 和 [延伸模組：停用所有延伸模組 (工作區)] 命令即可。

### <a name="enable-an-extension"></a>啟用擴充功能 

如果延伸模組已停用，則該延伸模組會出現在延伸模組清單的 [已停用] 區段中，並標示為 [已停用]。 您可使用下拉式功能表中的 [啟用] 或 [啟用 (工作區)] 命令來重新啟用延伸模組。 您也可以在 [命令選擇區] 使用 [延伸模組：啟用所有延伸模組] 和 [延伸模組：啟用所有延伸模組 (工作區)] 命令來啟用所有延伸模組。 

![延伸模組正在啟用](media/extensions/extensions-enable.png)

### <a name="updating-an-extension"></a>更新延伸模組

Azure Data Studio 會自動檢查所有已安裝的延伸模組並安裝更新。 如果想要關閉自動更新功能，則可使用 [延伸模組：停用自動更新延伸模組] 命令來停用自動更新。 

若要手動更新延伸模組，則可使用 [延伸模組：顯示過期的延伸模組] 命令來檢查延伸模組更新，此命令會使用 `@outdated` 篩選條件來搜尋延伸模組清單。 此動作會顯示所有目前已安裝延伸模組的可用更新。 按一下過期延伸模組上的 [更新] 按鈕，即會安裝更新。 系統會提示重新載入 Azure Data Studio。 您也可以使用 [延伸模組：更新所有延伸模組] 命令，同時更新所有過期的延伸模組。

[延伸模組：檢查延伸模組更新] 命令也是檢查延伸模組是否有可用更新的另一個方法。

## <a name="install-from-a-vsix"></a>從 VSIX 進行安裝

您可使用 [延伸模組] 檢視命令下拉式清單的 [從 VSIX 進行安裝] 命令，或使用 [命令選擇區] 中的 [延伸模組：從 VSIX 進行安裝] 命令，並指向該延伸模組的 `.vsix` 檔案，手動安裝封裝在 `.vsix` 檔案中的 Azure Data Studio 延伸模組。

## <a name="access-installed-azure-data-studio-extensions"></a>存取已安裝的 Azure Data Studio 延伸模組

每個延伸模組都會以不同方式強化您在 Azure Data Studio 中的體驗。 因此，延伸模組的進入點可能會有所不同。 請參閱已安裝延伸模組的個別文件，以取得安裝後如何存取其功能的資訊。

## <a name="extensions-view-filters"></a>延伸模組檢視篩選條件

[延伸模組] 檢視搜尋方塊可支援篩選，以協助尋找及管理延伸模組。 [顯示已安裝的延伸模組] 命令與 [顯示建議的延伸模組] 命令會在搜尋方塊中使用 `@installed` 和 `@recommended` 等篩選條件。

您可在 [延伸模組] 搜尋方塊中輸入 @，然後瀏覽建議，以查看所有篩選條件和排序命令的完整清單：

![延伸模組排序](media/extensions/extension-sort.png)

以下是 [延伸模組] 檢視的篩選：

- `@builtin` - 顯示 Azure Data Studio 隨附的延伸模組。 依類型分組 (程式設計語言、主題等)。
- `@disabled` - 顯示已停用的已安裝延伸模組。
- `@enabled` - 顯示已啟用的已安裝延伸模組。 延伸模組可個別啟用/停用。
- `@installed` - 顯示已安裝的延伸模組。
- `@outdated` - 顯示過期的已安裝延伸模組。 您可在 Marketplace 找到較新版本。
- `@recommended` - 顯示建議的延伸模組。 依特定工作區或一般用途分組。
- `@category` - 顯示屬於指定分類的延伸模組。 以下為幾個支援的類別。 如需完整清單，請輸入 @category，並遵循建議清單中的選項：
    - `@category:themes`
    - `@category:formatters`
    - `@category:snippets` 您也可以組合這些篩選條件。 例如，`@installed @category:themes` 會顯示所有已安裝的主題。

如果未提供篩選條件，則 [延伸模組] 檢視會顯示目前已安裝和建議的延伸模組。

### <a name="sorting"></a>排序 
您可使用 `@sort` 篩選條件來排序延伸模組，並採用下列值：

- `installs` - 依延伸模組庫安裝計數排序 (遞減)。
- `rating` - 依延伸模組庫評分 (1-5 顆星) 排序 (遞減)。
- `name` - 依延伸模組名稱的字母順序排序。

## <a name="common-questions"></a>常見問題

### <a name="where-are-extensions-installed"></a>延伸模組的安裝位置為何？ 
延伸模組會安裝在每個使用者的延伸模組資料夾中。 根據平台而定，該位置會位於下列資料夾：

- Windows `%USERPROFILE%\.azuredatastudio\extensions`
- macOS `~/.azuredatastudio/extensions`
- Linux `~/.azuredatastudio/extensions`
