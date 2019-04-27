---
title: 連接到資料來源 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.conndatasource.f1
ms.assetid: 1e2b17e9-092b-4af1-8a58-c52b8fe10ff1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 764884f73cb554794edfb998f2c8d7b8f8d7d1fe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680412"
---
# <a name="connect-to-a-data-source-ssas"></a>連接到資料來源 (SSAS)
  **[資料表匯入精靈]** 的這個頁面可讓您建立與各種資料來源之間的新資料來源連接，例如關聯式資料庫、資料摘要和檔案等資料來源。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 若要連接至資料來源，您必須先在機器上安裝適當的提供者。 您必須將適當的提供者安裝在工作空間資料庫伺服器上。 若是 32 位元 (x86) 伺服器，必須安裝 32 位元提供者。 若是 64 位元 (x64) 伺服器，必須安裝 64 位元提供者。  
  
 不管架構為何，[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 一律在 32 位元處理序下執行。 在 64 位元機器上執行 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 時，如果要安裝資料提供者，您應該注意下列事項：  
  
-   針對支援並行安裝 32 位元和 64 位元提供者的提供者，您必須同時安裝兩個提供者。  
  
-   至於 ACE 提供者，您必須安裝 64 位元版本的提供者。 由於 Office 會自動安裝 ACE 提供者，因此您不應該在裝載工作空間資料庫次無器的 64 位元機器上執行 32 位元版本的 Microsoft Office。  
  
     ACE 提供者用來從文字檔、Excel 檔和 Access 檔匯入。 如果不需要這些資料來源的支援，您可以在執行 64 位元工作空間資料庫伺服器的機器上，執行 32 位元版本的 Microsoft Office。  
  
-   針對不支援並行安裝 32 位元和 64 位元提供者的其他提供者，您必須安裝 32 位元提供者。 如果只有 64 位元機器可以使用，您必須使用遠端機器，並將 64 位元提供者安裝為工作空間資料庫伺服器。  
  
  
