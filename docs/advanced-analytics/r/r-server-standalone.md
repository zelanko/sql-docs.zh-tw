---
title: "R Server (獨立式) | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 06/22/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: ca9e48f1-67b8-4905-9b78-56752d7a4e81
caps.latest.revision: "22"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 1812dc6b60e5f5ee4547810a591b37643be17096
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="r-server-standalone"></a>R Server (Standalone)

SQL Server 2016 中，Microsoft 發行**R 伺服器 （獨立）**，它支援企業級分析的平台的一部分。  Microsoft R Server 提供延展性和安全性的 R 語言，並會解決開放原始碼 r 的記憶體限制SQL Server R 服務，例如 Microsoft R Server （獨立） 會提供平行和區塊處理的資料，讓 R 使用者使用遠大於可放入記憶體的資料。

在 SQL Server 2017，已新增支援的 Python 語言，喜歡的休閒活動學習、 機器社群中廣泛的支援，且包含常用的程式庫，針對文字分析和深入學習。  若要反映此更廣泛的語言設定，我們已也它重新命名為**Microsoft Machine Learning 伺服器 （獨立）**。

## <a name="benefits-of-microsoft-r-server"></a>Microsoft R Server 的優點

您可以使用 Microsoft R Server 的多個平台上的分散式運算。 當您安裝 SQL Server 安裝程式之外時，您取得 Windows 伺服器和所有必要的工具發行和部署模型。 如需其他平台的詳細資訊，請參閱 MSDN library 中的這些資源：

+ [Microsoft R Server 簡介 (英文)](https://msdn.microsoft.com/microsoft-r/rserver)
+ [R Server for Windows (英文)](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

您也可以安裝 Microsoft R Server 要做為開發用戶端，用來取得 RevoScaleR 程式庫和建立 R 解決方案，可部署到 SQL Server 所需的工具。

## <a name="whats-new-in-microsoft-machine-learning-server"></a>在 Microsoft Machine Learning 伺服器最新消息

如果您安裝的機器學習服務 （獨立） 使用 SQL Server 2017 安裝程式，您現在可以新增 Python 語言。 當然，R 語言仍然是支援的選項，而且您甚至可以視需要安裝這兩種語言。
 
在 SQL Server 2017 CTP 2.0 中，伺服器安裝也會包含 mrsdeploy 封裝和其他公用程式用於運用模型。 如需詳細資訊，請參閱[與 mrsdeploy 實施](../../advanced-analytics/operationalization-with-mrsdeploy.md)。

SQL Server 機器學習的企業使用者可以使用可下載的 Microsoft R Server 安裝程式升級他們的 R 元件，稱為繫結程序中。 如需詳細資訊，請參閱[使用 SqlBindR 升級到 SQL Server 執行個體](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

## <a name="get-microsoft-r-server-or-machine-learning-server-standalone"></a>取得 Microsoft R 伺服器或機器學習伺服器 （獨立）

 有多個 Microsoft R Server 安裝選項：

+ 使用 SQL Server 安裝精靈

  [建立獨立式 R Server](../r/create-a-standalone-r-server.md)

  執行 SQL Server 2016 安裝程式以安裝**Microsoft R Server （獨立）**。 預設會新增 R 語言。
  或者，執行 SQL Server 2017 安裝程式以安裝**機器學習伺服器 （獨立）**選取 R 或 Python，或兩者。

  > [!IMPORTANT]
  > 若要安裝的伺服器選項為**共用功能**安裝程式的區段。 不要安裝任何其他元件。
  >
  > 最好不要在已安裝 SQL Server R Services 或 SQL Server 機器學習服務的電腦上安裝伺服器。

+ 使用 SQL Server 安裝程式命令列選項

  [從命令列安裝 Microsoft R Server](../r/install-microsoft-r-server-from-the-command-line.md)

  SQL Server 安裝程式支援透過一組豐富的命令列引數的自動的安裝。

+ 使用獨立安裝程式

  [執行 Windows 的 Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。

  您現在可以使用新的 Windows 安裝程式來設定 Microsoft R Server 或 Microsoft Machine Learning 伺服器的新執行個體。  Microsoft R Server （和 Microsoft 機器學習 Server） 需要 SQL Server Enterprise 合約。 不過，在執行獨立安裝程式之後，現有安裝的支援原則會更新為使用新的現代化的生命週期原則。 此支援 選項可確保會比使用 SQL Server 版本更新服務時，其方式是經常套用機器學習服務元件的更新。

  
+ 升級 SQL Server 執行個體

  [若要升級的 R 服務執行個體使用 SqlBindR](./use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。
  
  您可以使用獨立安裝程式來升級 SQL Server 2016 使用 r 的最新版本的 R Services 的執行個體當您執行安裝程式時，現代化的生命週期支援原則會套用至伺服器，和 R 元件會更頻繁的更新。
  
  > [!請注意} 目前此更新方法是僅適用於現有的 SQL Server 2016 安裝。 不過，升級將會支援 SQL Server 2017 在未來。

## <a name="related-machine-learning-products"></a>相關的機器學習的產品

+ 使用 R Server 的 azure 虛擬機器

  [佈建的 R 伺服器虛擬機器](../../advanced-analytics/r-services/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  Azure marketplace 包含多個虛擬機器映像，包括 R 伺服器。 在 Microsoft Azure 中建立新的 R Server 虛擬機器是最快速的方式設定伺服器，以用於開發和部署預測模型。 映像隨附於調整及共用已設定，使其更容易內嵌 R 分析應用程式內，以及整合 R 與後端系統的功能。

+ Data Science 虛擬機器

  [Data Science 虛擬機器 Windows 2016 Preview](http://aka.ms/dsvm/win2016)

  資料科學虛擬機器的最新版本包括 R 伺服器、 SQL Server，加上最受歡迎的機器學習工具陣列所有預先安裝，並測試。 建立 Jupyter 筆記本，來開發方案 Julia，並使用如 MXNet、 CNTK，以及 TensorFlow GPU 啟用深入學習程式庫。

## <a name="resources"></a>資源

範例、 教學課程中，與 Microsoft R Server 的詳細資訊，請參閱[Microsoft R 產品](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started)。

## <a name="see-also"></a>請參閱＜

 [SQL Server R 服務](../../advanced-analytics/r/sql-server-r-services.md)

