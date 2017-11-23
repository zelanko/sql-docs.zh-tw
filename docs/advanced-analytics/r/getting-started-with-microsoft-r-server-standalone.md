---
title: "開始使用 Microsoft R Server (獨立式) | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: a0932e10c72166bee4b674ea5df6e80b032e7964
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="getting-started-with-machine-learning-server-standalone"></a>開始使用機器學習 Server （獨立）
 
在 SQL Server 2016 中，Microsoft R Server （獨立） 幫助熱門的開放原始碼 R 語言帶入企業中，以便啟用高效能分析方案以及與其他商務應用程式整合。  

在 SQL Server 2017，名稱已變更為以反映 Python 語言支援新增機器學習伺服器 （獨立）。 這兩個版本可免費至 Enterprise Edition 或軟體保證的使用者。

本文章提供如何使用機器學習伺服器 （或 R 伺服器），以及如何開始安裝及範例的高階概觀。

## <a name="why-use-a-standalone-server-for-machine-learning"></a>為什麼使用機器學習的獨立伺服器

如果您不需要整合您的機器學習解決方案與 SQL Server 資料，機器學習伺服器可讓您的 R 和 Python，相同的分散式、 可調整支援，此外支援 Hadoop、 Spark 或 Linux 的解決方案部署。

機器學習伺服器也會包含影像分析和情緒分析，您可以立即使用應用程式中預先定型的模型。

機器學習服務伺服器的實施功能支援部署與使用 web 服務與遠端執行，叢集拓撲 Spark 與 Hadoop MapReduce 散發 R，並將 Python 的解決方案，以及支援適用於 Windows 或 Linux。

**SQL Server 2016**

+ 安裝 Microsoft R Server （獨立） 從 SQL Server 2016 安裝程式。

    此選項會建立完全獨立於 R 服務 （資料庫） 的獨立伺服器。 此版本只支援 R。 獨立伺服器安裝隨附於您的 SQL Server Enterprise Edition 支援原則。 如需詳細資訊，請參閱[建立獨立式 R Server](../../advanced-analytics/r/create-a-standalone-r-server.md)。

+ 安裝 R Server 使用個別的 Windows 安裝程式。

    此安裝程式會建立使用 Microsoft 現代軟體生命週期支援原則的 Microsoft R Server 的新執行個體。 您也可以安裝 R Server 適用於 Linux、 Cloudera、 Teradata 和 Hadoop。
    
    如需詳細資訊，請參閱[適用於 Windows 安裝 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

**SQL Server 2017**

+ 安裝機器學習伺服器 （獨立） 從 SQL Server 2017 安裝程式。 

    此選項會建立獨立伺服器，以支援實施機器學習中 R、 Python 或兩者。 獨立伺服器安裝隨附於您的 SQL Server Enterprise Edition 支援原則。 如需詳細資訊，請參閱[建立獨立式 R Server](../../advanced-analytics/r/create-a-standalone-r-server.md)。  

+ 使用新的獨立 Windows 安裝程式。

    此安裝方法建立機器學習使用之伺服器的 Microsoft 現代軟體生命週期支援原則的新執行個體。 您也可以安裝在 Hadoop、 Spark 或 Linux 的機器學習伺服器不需要額外成本。
    
    如需詳細資訊，請參閱[安裝機器學習 Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

**升級現有的伺服器**

+ 如果您有現有的伺服器或您想要升級的執行個體，請下載並執行 windows 安裝程式取得更新。 

    如需詳細資訊，請參閱[升級執行個體的使用 SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="start-using-machine-learning-server"></a>開始使用機器學習伺服器

 您已設定伺服器元件，並設定您的 IDE 使用機器學習伺服器二進位檔之後，您可以開始開發使用新的 Api，例如 RevoScaleR 和 revoscalepy、 MicrosoftML，以及 olapR 方案。
    
若要開始，請參閱這些指南：

+ [方案範本](https://docs.microsoft.com/machine-learning-server/r/sample-solutions)

    這些範例是示範如何套用在特定產業中的機器學習的解決方案。 目前的案例是在零售、 財務、 衛生保健、 和行銷。

+ [R 和 ScaleR 25 函式中的，瀏覽](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)： 瀏覽此集合提供高效能和縮放 R 解決方案的 「 可散布分析函數。 包含許多最熱門 R 模型建立套件 (例如 	K-Means 叢集、決策樹及決策樹系) 的可平行處理版本，以及資料操作工具。

- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx)

    MicrosoftML 套件是機器的一組新學習演算法和轉換會在 Microsoft 開發的快速和可擴充。 您可以在 R 或 Python 來使用它。 如需詳細資訊，請參閱[python MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)和[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)。

## <a name="see-also"></a>另請參閱

[開始使用 SQL Server 機器學習服務](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)