---
title: 安裝和解除安裝 OData 來源元件 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ae48af3dec0be31d329548cbc0d7cd76007dacaf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030088"
---
# <a name="install-and-uninstall-odata-source-component"></a>安裝及解除安裝 OData 來源元件
  本主題提供在電腦上安裝或移除 OData 來源元件的指示。  
  
## <a name="installation"></a>安裝  
 OData 來源元件要求必須在電腦上安裝以下必要元件。  
  
-   SQL Server Data Tools (為了設計封裝)  
  
-   SQL Server Integration Services (為了在 Visual Studio 外面執行封裝)  
  
 若要安裝 OData 來源元件，請下載[SQL Server 2014 功能套件](http://go.microsoft.com/fwlink/p/?LinkId=391999)並執行其中一個下列 MSI 檔案。  
  
-   64 位元平台適用的 ODataSourceForSQLServer2014-amd64.msi  
  
-   32 位元平台適用的 ODataSourceForSQLServer2014-x86.msi  
  
> [!IMPORTANT]  
>  64 位元安裝程式將會同時安裝 32 位元和 64 位元版的 OData 來源元件。 如果您使用 32 位元作業系統，您只需要執行 32 位元的安裝程式。  
  
## <a name="uninstallation"></a>解除安裝  
 可以從解除安裝 OData 來源元件**程式和功能**功能表。 尋找**Microsoft SQL Server SSIS OData 來源元件 (x64)** 項目，並按一下**解除安裝**。  
  
  