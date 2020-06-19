---
title: 安裝和卸載 OData 來源元件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
author: janinezhang
ms.author: janinez
ms.openlocfilehash: eeeea240761915fae8489072cc71d697b988ce7e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965458"
---
# <a name="install-and-uninstall-odata-source-component"></a>安裝及解除安裝 OData 來源元件
  本主題提供在電腦上安裝或移除 OData 來源元件的指示。  
  
## <a name="installation"></a>安裝  
 OData 來源元件要求必須在電腦上安裝以下必要元件。  
  
-   SQL Server Data Tools (為了設計封裝)  
  
-   SQL Server Integration Services (為了在 Visual Studio 外面執行封裝)  
  
 若要安裝 OData 來源元件，請下載[SQL Server 2014 功能套件](https://go.microsoft.com/fwlink/p/?LinkId=391999)，然後執行下列其中一個 MSI 檔案。  
  
-   64 位元平台適用的 ODataSourceForSQLServer2014-amd64.msi  
  
-   32 位元平台適用的 ODataSourceForSQLServer2014-x86.msi  
  
> [!IMPORTANT]  
>  64 位元安裝程式將會同時安裝 32 位元和 64 位元版的 OData 來源元件。 如果您使用 32 位元作業系統，您只需要執行 32 位元的安裝程式。  
  
## <a name="uninstallation"></a>解除安裝  
 您可以從 [**程式和功能**] 功能表中卸載 OData 來源元件。 尋找 [ **MICROSOFT SQL SERVER SSIS OData 來源元件（x64）** ] 專案，然後按一下 [**卸載**]。  
  
  
