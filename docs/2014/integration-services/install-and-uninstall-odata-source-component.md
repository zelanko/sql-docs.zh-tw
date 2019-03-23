---
title: 安裝和解除安裝 OData 來源元件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 34a71ed768c49436a4dba4ecf225bdd009132866
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385256"
---
# <a name="install-and-uninstall-odata-source-component"></a>安裝及解除安裝 OData 來源元件
  本主題提供在電腦上安裝或移除 OData 來源元件的指示。  
  
## <a name="installation"></a>安裝  
 OData 來源元件要求必須在電腦上安裝以下必要元件。  
  
-   SQL Server Data Tools (為了設計封裝)  
  
-   SQL Server Integration Services (為了在 Visual Studio 外面執行封裝)  
  
 若要安裝 OData 來源元件，下載[SQL Server 2014 功能套件](https://go.microsoft.com/fwlink/p/?LinkId=391999)並執行其中一個下列的 MSI 檔案。  
  
-   64 位元平台適用的 ODataSourceForSQLServer2014-amd64.msi  
  
-   32 位元平台適用的 ODataSourceForSQLServer2014-x86.msi  
  
> [!IMPORTANT]  
>  64 位元安裝程式將會同時安裝 32 位元和 64 位元版的 OData 來源元件。 如果您使用 32 位元作業系統，您只需要執行 32 位元的安裝程式。  
  
## <a name="uninstallation"></a>解除安裝  
 從可以解除安裝 OData 來源元件**程式和功能**功能表。 尋找**Microsoft SQL Server SSIS OData 來源元件 (x64)** 項目，然後按一下**解除安裝**。  
  
  
