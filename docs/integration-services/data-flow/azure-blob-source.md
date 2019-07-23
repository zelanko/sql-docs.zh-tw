---
title: Azure Blob 來源 | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobsrc.f1
- sql14.dts.designer.afpblobsrc.f1
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2b90f56f69aed9da7194f2a95b0fa9598db0da50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045449"
---
# <a name="azure-blob-source"></a>Azure Blob 來源

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Azure Blob 來源** 元件可讓 SSIS 封裝從 Azure Blob 讀取資料。 支援的檔案格式：CSV 和 AVRO。
  
  若要查看 Azure Blob 來源的編輯器，可在資料流程設計師上拖放 **Azure Blob 來源** ，並連按兩下以開啟編輯器。  
  
 **Azure Blob 來源**是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。  
  
1.  針對 [Azure 儲存體連線管理員]  欄位，請指定現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員。  
  
2.  針對 [Blob 容器名稱]  欄位，請指定包含原始程式檔的 Blob 容器名稱。  
  
3.  針對 [Blob 名稱]  欄位，請指定 Blob 的路徑。  
  
4.  針對 [Blob 檔案格式]  欄位，請指定要使用 [文字]  或 [Avro]  的 Blob 格式。  
  
5.  檔案格式若為 [文字]  ，則您必須指定 [資料行分隔符號字元]  值。 (不支援多字元分隔符號)。

    若檔案中第一個資料列包含資料行名稱，請選取 [第一個資料列的資料行名稱]  。

6.  如果檔案已壓縮，請選取 [解壓縮檔案]  。

7.  如果檔案已壓縮，請選取 [壓縮類型]  ：**GZIP**、**DEFLATE** 或 **BZIP2**。 請注意，不支援 Zip 格式。
  
8.  指定連線資訊後，請切換至 [資料行]  頁面，將來源資料行對應至 SSIS 資料流程的目的地資料行。  
  
  
