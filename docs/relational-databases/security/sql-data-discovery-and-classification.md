---
title: SQL 資料探索與分類 | Microsoft Docs
description: SQL 資料探索與分類
documentationcenter: ''
ms.reviewer: carlrab
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.prod_service: sql-database,sql
ms.custom: security
ms.topic: conceptual
ms.date: 02/13/2018
ms.author: giladm
author: giladm
manager: shaik
ms.openlocfilehash: c3c9936c7a69ec2d4f54f1f4412c5b39f60035e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47607096"
---
# <a name="sql-data-discovery-and-classification"></a>SQL 資料探索與分類
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

資料探索與分類引進內建至 SQL Server Management Studio (SSMS) 的新工具，以**探索**、**分類**、**標示**和 & **報告**您資料庫中的敏感性資料。
探索和分類最敏感的資料 (商務、財務、醫療等等) 可以扮演組織資訊保護成長的關鍵角色。 它可以作為下列的基礎結構：
* 協助符合資料隱私權標準。
* 控制存取以及強化包含高敏感性資料之資料庫/資料行的安全性。

> [!NOTE]
> **SQL Server 2008 和更新版本支援**資料探索與分類。 針對 Azure SQL Database，請參閱 [Azure SQL Database 資料探索與分類](https://go.microsoft.com/fwlink/?linkid=866265)。

## <a id="subheading-1"></a>概觀
資料探索與分類引進一組進階服務，形成目標為保護資料的新 SQL Information Protection 範例，而不只是資料庫：
* **探索與建議** - 分類引擎會掃描您的資料庫，並識別包含潛在敏感性資料的資料行。 它接著可讓您輕鬆地檢閱並套用適當的分類建議，以及手動分類資料行。
* **標記** - 在資料行上可以持續標示敏感度分類標籤。
* **可見性** - 資料庫分類狀態可以在詳細報表中進行檢視，而詳細報表可以進行列印/匯出，以用於合規性和稽核用途，以及其他需要。

## <a id="subheading-2"></a>探索、分類和標示敏感資料行
下節所描述的步驟是有關探索、分類和標示包含您資料庫中敏感性資料的資料行，以及檢視資料庫的目前分類狀態，並匯出報表。

分類包含兩個中繼資料屬性：
* 標籤 - 主分類屬性，用來定義資料行中所儲存資料的敏感度等級。  
* 資訊類型 - 提供資料行中所儲存資料類型的額外細微性。

<br>
**分類 SQL Server 資料庫：**

1. 在 SQL Server Management Studio (SSMS) 中，連線至 SQL Server。

2. 在 SSMS 物件總管中，以滑鼠右鍵按一下您想要分類的資料庫，然後選擇 [工作] > [分類資料...]。

    ![瀏覽窗格][1]

3. 分類引擎會掃描您資料庫中是否有資料行包含潛在敏感度資料，並提供**建議的資料行分類**清單：

    * 若要檢視建議的資料行分類清單，請按一下頂端的建議通知方塊或視窗底部的建議面板：

        ![瀏覽窗格][2]

        ![瀏覽窗格][3]

    * 檢閱建議清單：
        * 若要接受特定資料行的建議，請核取相關資料列左側資料行中的核取方塊。 您也可以核取建議資料表標頭中的核取方塊，以將「所有建議」標記為已接受。

        * 您也可以使用下拉式方塊來變更建議的「資訊類型」和「敏感度標籤」。        

        ![瀏覽窗格][4]

    * 若要套用選取的建議，請按一下藍色的 [Accept selected recommendations] (接受選取的建議) 按鈕。

        ![瀏覽窗格][5]

4. 您也可以**手動分類**資料行作為 (以及) 建議分類的替代方法：

    * 按一下視窗上方功能表中的 [新增分類]。

        ![瀏覽窗格][6]

    * 在開啟的內容視窗中，選取結構描述 > 資料表 > 您想要分類的資料行，以及資訊類型和敏感度標籤。 然後按一下內容視窗底部的藍色 [新增分類] 按鈕。

        ![瀏覽窗格][7]

5. 若要完成您的分類，並使用新的分類中繼資料持續標示 (標記) 資料庫資料行，請按一下視窗上方功能表中的 [儲存]。

    ![瀏覽窗格][8]


6. 若要產生具有完整資料庫分類狀態摘要的報表，請按一下視窗上方功能表中的 [檢視報告]。

    ![瀏覽窗格][9]

    ![瀏覽窗格][10]


## <a id="subheading-3"></a>存取分類中繼資料

「資訊類型」和「敏感度標籤」的分類中繼資料會儲存在下列擴充屬性中： 
* sys_information_type_name
* sys_sensitivity_label_name

您可以使用擴充屬性目錄檢視 [sys.extended_properties](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties) 來存取中繼資料。

下列程式碼範例會傳回所有的分類資料行，以及其對應的分類：

```sql
SELECT
    schema_name(O.schema_id) AS schema_name,
    O.NAME AS table_name,
    C.NAME AS column_name,
    information_type,
    sensitivity_label 
FROM
    (
        SELECT
            IT.major_id,
            IT.minor_id,
            IT.information_type,
            L.sensitivity_label 
        FROM
        (
            SELECT
                major_id,
                minor_id,
                value AS information_type 
            FROM sys.extended_properties 
            WHERE NAME = 'sys_information_type_name'
        ) IT 
        FULL OUTER JOIN
        (
            SELECT
                major_id,
                minor_id,
                value AS sensitivity_label 
            FROM sys.extended_properties 
            WHERE NAME = 'sys_sensitivity_label_name'
        ) L 
        ON IT.major_id = L.major_id AND IT.minor_id = L.minor_id
    ) EP
    JOIN sys.objects O
    ON  EP.major_id = O.object_id 
    JOIN sys.columns C 
    ON  EP.major_id = C.object_id AND EP.minor_id = C.column_id
```

## <a id="subheading-4"></a>後續步驟

針對 Azure SQL Database，請參閱 [Azure SQL Database 的資料探索與分類](https://go.microsoft.com/fwlink/?linkid=866265)。

請考慮套用資料行層級安全性機制來保護敏感資料行：

* [動態資料遮罩](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking)以模糊化使用中的敏感資料行。
* [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) 以加密靜止的敏感資料行。

<!--Anchors-->
[SQL Data Discovery & Classification overview]: #subheading-1
[Discovering, classifying & labeling sensitive columns]: #subheading-2
[Accessing the classification metadata]: #subheading-3
[Next Steps]: #subheading-4

<!--Image references-->
[1]: ./media/sql-data-discovery-and-classification/1_data_classification_explorer_menu.png
[2]: ./media/sql-data-discovery-and-classification/2_recommendations_notification_box.png
[3]: ./media/sql-data-discovery-and-classification/3_recommendations_panel.png
[4]: ./media/sql-data-discovery-and-classification/4_recommendations.png
[5]: ./media/sql-data-discovery-and-classification/5_accept_recommendations_button.png
[6]: ./media/sql-data-discovery-and-classification/6_add_classification_button.png
[7]: ./media/sql-data-discovery-and-classification/7_manual_classification.png
[8]: ./media/sql-data-discovery-and-classification/8_save.png
[9]: ./media/sql-data-discovery-and-classification/9_view_report.png
[10]: ./media/sql-data-discovery-and-classification/10_report.png
