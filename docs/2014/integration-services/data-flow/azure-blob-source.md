---
title: Azure Blob 來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobsrc.f1
- sql11.dts.designer.afpblobsrc.f1
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9feb14f98bec3a1a48526d2c3c72641ad61c48e9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380276"
---
# <a name="azure-blob-source"></a>Azure Blob 來源
 **Azure Blob 來源** 元件可讓 SSIS 封裝從 Azure Blob 讀取資料。 支援的檔案格式：CSV 和 AVRO。 若要查看 Azure Blob 來源的編輯器，可在資料流程設計師上拖放 **Azure Blob 來源** ，並連按兩下以開啟編輯器。  
  
1.  針對 [Azure 儲存體連線管理員] 欄位，請指定現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員。  
  
2.  針對 [Blob 容器名稱] 欄位，請指定包含原始程式檔的 Blob 容器名稱。  
  
3.  針對 [Blob 名稱] 欄位，請指定 Blob 的路徑。  
  
4.  針對 [Blob 檔案格式] 欄位，請指定要使用的 Blob 格式。  
  
5.  若檔案格式為 CSV，則您必須指定 [資料行分隔符號字元] 值。 若檔案中第一個資料列包含資料行名稱，請選取 [第一個資料列的資料行名稱]。  
  
6.  指定連接資訊後，請切換至 [資料行]  頁面，將來源資料行對應至 SSIS 資料流程的目的地資料行。  
  
  
