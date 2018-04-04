---
title: 安裝及管理 SQL Server 中的機器學習封裝 |Microsoft 文件
ms.custom: ''
ms.date: 02/19/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 9b2bf101674d6733c137324c9e5581647251726b
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="installing-and-managing-machine-learning-packages-in-sql-server"></a>安裝及管理 SQL Server 中的機器學習封裝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何安裝新的 R 或 Python 封裝，在 SQL Server 2017 和 SQL Server 2016 中。 它也會描述您可以在 SQL Server 安裝的封裝上的限制。

## <a name="overview-of-package-management-methods-and-requirements"></a>封裝管理方法 」 和 「 需求概觀

不同於一般 R 或 Python 開發，必須安裝 SQL Server 所使用的封裝至系統管理控制下的資料夾。 有許多優點，讓封裝在單一位置：

+ 伺服器系統管理員可以監視新增新的檔案和程式庫的伺服器上，以及控制使用封裝程式庫檔案的成長。 
+ 封裝可以更輕鬆地共用多個資料庫使用者，而不是在使用者程式庫中安裝多份相同的封裝。
+ 可以安裝只受保護的、 已核准的套件，來保護伺服器和其作業。

不過，這些限制一定會表示某些變更的資料科學家和分析師運作的方式：

+ 一般而言，系統管理伺服器的存取權是必要的。 在 SQL Server 2017，資料庫管理員可以使用角色來授與特定使用者能夠安裝套件的私用，但系統管理員仍必須啟用此功能。
+ 許多伺服器沒有網際網路存取。 封裝安裝至這些電腦需要一些額外的準備工作。
+ 封裝會安裝至執行個體文件庫。 封裝無法執行個體之間共用。
+ 使用者無法執行任何已安裝在使用者程式庫中的封裝。

## <a name="package-installation-guides-for-r-or-python"></a>R 或 Python 封裝安裝指南

有關如何安裝新的 R 或 Python 封裝，請參閱下列文章以取得詳細的步驟。 

### <a name="install-new-r-packages"></a>安裝新的 R 封裝

+ [SQL Server 上安裝其他的 R 封裝](install-additional-r-packages-on-sql-server.md)

    您可以在 SQL Server 2016 或 2017年上安裝 R 封裝，以系統管理員身分，使用的 R 工具。

    您也可以從遠端的 R 用戶端安裝 R 封裝，R Server 9.0.2 安裝或更新。

    您也可以使用 DDL 陳述式的 SQL Server 2017 中安裝 R 封裝。

### <a name="install-new-python-packages"></a>安裝新的 Python 封裝

+ [在 SQL Server 上安裝新的 Python 套件](../python/install-additional-python-packages-on-sql-server.md)

## <a name="prerequisites"></a>필수 구성 요소

您嘗試下載或安裝任何新的封裝之前，先檢閱需求：

+ 請確定 Windows 版本的套件：[取得正確的封裝版本和格式](#packageVersion)

+ 找出所有套件相依性，並確定其與 SQL Server 環境的相容性。

+ 請確認 R 版本或 Python 版本相容性。 套件必須與 R 」 或 「 執行 SQL Server 中的 Python 版本相容。

+ 權限。 判斷您是否需要安裝封裝的權限。 若要安裝到執行個體文件庫，請執行 SQL Server 之電腦的系統管理權限。 如果您沒有 SQL Server 電腦的系統管理權限，尋找 封裝安裝協助資料庫管理員。

    在 SQL Server 2017，您可以從遠端用戶端，安裝 R 封裝，如果封裝管理已啟用伺服器上，而且您是資料庫擁有者或封裝管理角色的成員。

+ 請考慮的風險和特定的封裝安裝到 SQL Server 環境的優點。 檢查封裝 （或任何它所需要的套件） 包含 SQL Server 或原則會遭到封鎖的功能。 許多 R，並將 Python 封裝會強行寫入的 SQL Server 環境非常適合。 問題可能包括：

    - 存取網路的封裝
    - 需要 Java 或不常使用的 SQL Server 環境中的其他架構封裝
    - 需要提高權限的檔案系統存取的封裝
    - 封裝適用於 web 程式開發或不在 SQL Server 內執行獲益的其他工作。

## <a name="installation-on-servers-with-no-internet-access"></a>在沒有網際網路存取的伺服器上安裝

一般情況下，裝載生產資料庫的伺服器不允許連線到網際網路。 在這類環境中安裝新的 R 或 Python 封裝需要您事先準備的所有封裝和其相依性，並將檔案複製到安裝中使用的伺服器上的資料夾。

1. 找出所有套件相依性。 
2. 請檢查任何必要的封裝是否已安裝在伺服器上。 如果已安裝此套件，請確認版本是否正確。
3. 下載封裝和所有相依性到另一部電腦。
4. 檔案伺服器移至可存取的資料夾。
5. 執行支援的安裝命令或 DDL 陳述式，將封裝安裝到執行個體文件庫。

識別所有相依性可能很複雜。 ，我們建議您使用[miniCRAN](create-a-local-package-repository-using-minicran.md)準備離線封裝儲存機制。

Python，您必須同樣地準備所有相依性，並將它們儲存在本機。 請務必使用 Windows 相容的二進位檔案，並使用 WHL 格式。
