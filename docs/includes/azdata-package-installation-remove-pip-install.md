---
author: MikeRayMSFT
ms.prod: sql
ms.topic: include
ms.date: 01/07/2020
ms.author: mikeray
ms.openlocfilehash: 401d214495cd8df8ec3401c0b18db8ebe8773226
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75721526"
---
### <a name="pythonpip-installation"></a>Python/Pip 安裝

您可以使用 yum、apt 或 zypper 在 Linux 上安裝 `azdata`，或使用 Homebrew 安裝套件管理員在 MacOS 上安裝。 您必須先安裝必要的 Python 與 pip，才能開始使用這些套件管理員。

>[!IMPORTANT]
>在繼續之前，您必須先移除已安裝到全域系統 Python 的任何 `azdata` 安裝。 新的安裝程式或原生套件會將 `azdata` 新增到您的路徑，而且不可能知道哪一個是第一個。
如果您已將現有的 `azdata` 安裝到全域系統 Python，請先將其移除再繼續。

若要檢視目前的安裝，請執行下列命令：

```bash
$ pip list --format columns
```

若 `azdata` 是由 pip 安裝，則會傳回套件與版本。 例如：

```
 Package             Version
------------------- ----------
azdata-cli          15.0.X
azdata-cli-app      15.0.X
azdata-cli-cluster  15.0.X
azdata-cli-core     15.0.X
azdata-cli-hdfs     15.0.X
azdata-cli-notebook 15.0.X
azdata-cli-profile  15.0.X
azdata-cli-spark    15.0.X
azdata-cli-sql      15.0.X
```

下列範例會移除 `azdata` 的 pip 安裝。

```bash
$ pip freeze | grep azdata-* | xargs pip uninstall -y
```

確認已移除使用 pip 安裝的任何 `azdata` 安裝之後，請繼續安裝。