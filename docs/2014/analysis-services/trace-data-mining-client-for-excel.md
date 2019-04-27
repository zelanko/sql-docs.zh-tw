---
title: 追蹤 （適用於 Excel 的資料採礦用戶端） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tracer
- connections
ms.assetid: 4aea3e17-cd0f-48dd-8f22-b54a6c716426
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 688357b2357cba8fa868eca18b5c100cfff1722d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62756457"
---
# <a name="trace-data-mining-client-for-excel"></a>追蹤 (適用於 Excel 的資料採礦用戶端)
  ![追蹤按鈕](media/misc-trace.gif "追蹤按鈕")  
  
 **追蹤** 對話方塊可協助您監視傳送至執行個體的陳述式[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]要用於資料採礦。 您已建立的執行個體的連接之後[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，用戶端與伺服器之間的所有互動都會都記錄在**追蹤** 窗格中，包括建立結構、 加入採礦模型，以及進行的陳述式預測，以及從伺服器傳回的一些訊息。  
  
 根據要求的動作，陳述式可能是資料採礦延伸模組 (DMX) 資料定義查詢或資料操作查詢、Analysis Services 指令碼語言 (ASSL) 封包，或 Analysis Services 預存程序的呼叫。 但是，實際的數值結果和資料值則不會顯示。  
  
 **追蹤**監視只為目前的連線，以及內容**追蹤**對話方塊不會儲存。  
  
## <a name="options"></a>選項。  
 追蹤窗格  
 列出從 Excel 用戶端傳送到伺服器的所有陳述式。  
  
 根據要求的動作，陳述式可能是 DMX 資料操作或資料定義陳述式、Analysis Services 預存程序的呼叫，或 XML/A 封包。  
  
 **目前的連接**  
 按一下以顯示目前連接的定義。 定義會包含連接的名稱、提供者、資料來源、目錄、交易上次使用連接的時間，以及目前的狀態 (開啟、非使用中)。  
  
 **使用工作階段模型**  
 選取此核取方塊，便會在伺服器上將資料採礦模型和結構儲存為暫存物件。 您所建立的模型和結構僅在進行目前的工作階段時可以使用。  
  
 取消選取此選項就可以將模型或結構存放在 Analysis Services 伺服器上進行儲存。  
  
 **請注意**您使用適用於 Excel 的資料表分析工具時，才能夠使用暫存物件是可用。 Visio 資料採礦範本與適用於 Excel 的資料採礦用戶端都需要使用結構和模型，才能存放在伺服器上。  
  
## <a name="tracing-temporary-structures-and-models"></a>追蹤暫時性結構和模型  
 如果您要使用預設會建立暫時性結構和模型的資料表分析工具，伺服器與用戶端之間的活動會受到監視，但是您所建立的模型或結構不會永久儲存到伺服器。  
  
 如果您想要保留您的工作，使用其中一個資料表分析工具時，您可以取消選取該選項**使用工作階段模型**，以讓您的模型永久儲存在伺服器上。 您也可以複製中的陳述式**追蹤**窗格中的檔案，以便稍後您可以重新建立您的工作。  
  
## <a name="understanding-sessions"></a>了解工作階段  
 當您連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體時，此資料採礦增益集會起始工作階段。 每一個工作階段都會收到一個工作階段識別碼，此識別碼會識別 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上現有的工作階段。 但是，工作階段識別碼並不保證工作階段會維持有效狀態。 如果工作階段逾時或是與工作階段有關的連接中斷，則此工作階段會過期。 如果此工作階段過期而不再有效，則 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會結束此工作階段，並回復進行中的任何交易。 如果訊息傳送時附有不再有效的工作階段識別碼，則該訊息會失敗且出現錯誤，表示找不到指定的工作階段。  
  
 雖然某些資料採礦模型會明確地儲存在伺服器上，但工作階段採礦模型和結構並不會，而且工作階段資料採礦活動也不會保存任何記錄。 由於暫存的採礦模型和結構會在您結束工作階段後立即刪除，所以在儲存您要保留的任何工作之前，請避免關閉 Excel 活頁簿。  
  
## <a name="changing-connections"></a>變更連接  
 變更連接並不會刪除之前連接的追蹤， 只有關閉活頁簿會清除工作階段。  
  
 如果您在 Excel 活頁簿中工作時變更連接，連接的變更不會記錄在**追蹤**窗格。 若要明確顯示目前連接的狀態與名稱，您必須按一下**目前的連接**。  
  
## <a name="understanding-statements-in-the-tracer"></a>了解 Tracer 中的陳述式  
 DMX 是一種語言，您可用它來建立及處理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的資料採礦模型。 您可以使用 DMX 建立新資料採礦模型的結構、定型這些模型，以及瀏覽、管理與預測模型。 DMX 是由資料定義語言 (DDL) 陳述式、資料操作語言 (DML) 陳述式及函數和運算子所組成。  
  
 DMX 陳述式的完整討論以及其語法不在本主題的討論範圍內。 不過，您可以使用中的資訊**追蹤**窗格，即可找到的 DMX 陳述式行為的詳細的資訊。 適用於 Excel 的資料採礦增益集也可以協助您建立複雜的 DMX 陳述式以及與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器互動。 如需詳細資訊，請參閱 <<c0> [ 查詢&#40;SQL Server 資料採礦增益集&#41;](query-sql-server-data-mining-add-ins.md)。</c0>  
  
> [!NOTE]  
>  許多 DMX 陳述式都經過參數化。 如果是簡單的類型，參數的值會列在陳述式下方。 不過如果是複雜的類型，則只會列出參數的類型。  
  
 SQL Server Analysis Services 也會使用 XML for Analysis (XMLA) 通訊協定來處理用戶端應用程式之間的所有通訊，這些應用程式包括適用於 Excel 的資料採礦用戶端和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體。  
  
 如需有關 DMX 語法，以及 XMLA 中命令和元素的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》。  
  
 傳送到伺服器的某些陳述式可能包括呼叫 Analysis Services 系統預存程序的查詢。 如需詳細資訊，請參閱《SQL Server 線上叢書》。  
  
  
