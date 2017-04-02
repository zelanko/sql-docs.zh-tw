---
title: "與巢狀 FOR XML 查詢比較的 FOR XML 查詢 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR XML 查詢"
  - "查詢 [SQL Server 中的 XML], 比較查詢類型"
ms.assetid: 19225b4a-ee3f-47cf-8bcc-52699eeda32c
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# 與巢狀 FOR XML 查詢比較的 FOR XML 查詢
  本主題會將單一層 FOR XML 查詢與巢狀 FOR XML 查詢做比較。 使用巢狀 FOR XML 查詢的其中一個好處，就是可以針對查詢結果指定屬性中心及元素中心 XML 的組合。 以下範例將提供示範。  
  
## 範例  
 下列 `SELECT` 查詢會擷取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中的產品類別目錄及子類別目錄資訊。 此查詢中沒有巢狀的 FOR XML。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductCategory.ProductCategoryID,   
         ProductCategory.Name as CategoryName,  
         ProductSubCategory.ProductSubCategoryID,   
         ProductSubCategory.Name  
FROM     Production.ProductCategory, Production.ProductSubCategory  
WHERE    ProductCategory.ProductCategoryID = ProductSubCategory.ProductCategoryID  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
GO  
```  
  
 以下是部份結果：  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory ProductSubCategoryID="1" Name="Mountain Bike"/>  
  <ProductSubCategory ProductSubCategoryID="2" Name="Road Bike"/>  
  <ProductSubCategory ProductSubCategoryID="3" Name="Touring Bike"/>  
</ProductCategory>  
...  
```  
  
 如果在查詢中指定 `ELEMENTS` 指示詞，會收到元素中心的結果，如以下結果片段所示：  
  
```  
<ProductCategory>  
  <ProductCategoryID>1</ProductCategoryID>  
  <CategoryName>Bike</CategoryName>  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <Name>Mountain Bike</Name>  
  </ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  </ProductSubCategory>  
</ProductCategory>  
```  
  
 接下來，假設您想要產生 XML 階層，結合屬性中心及元素中心的 XML，如以下片段所示：  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 在前述片段中，類別目錄識別碼及類別目錄名稱等產品類別目錄資訊為屬性。 但是，子類別目錄資訊是元素中心的。 若要建構 <`ProductCategory`> 元素，您可以撰寫 `FOR XML` 查詢，如下所示：  
  
```  
SELECT ProductCategoryID, Name as CategoryName  
FROM Production.ProductCategory ProdCat  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 以下是結果：  
  
```  
< ProdCat ProductCategoryID="1" CategoryName="Bikes" />  
< ProdCat ProductCategoryID="2" CategoryName="Components" />  
< ProdCat ProductCategoryID="3" CategoryName="Clothing" />  
< ProdCat ProductCategoryID="4" CategoryName="Accessories" />  
```  
  
 若要在希望的 XML 中建構巢狀的 <`ProductSubCategory`> 元素，您可以接著加入巢狀 `FOR XML` 查詢，如下所示：  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName  
        FROM   Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 下列為上一個查詢的注意事項：  
  
-   內部 `FOR XML` 查詢會擷取產品子類別目錄資訊。 在內部 `ELEMENTS` 中加入 `FOR XML` 指示詞，以產生元素中心的 XML，此 XML 已加入至外部查詢產生的 XML 中。 根據預設，外部查詢會產生屬性中西的 XML。  
  
-   在內部查詢中指定 `TYPE` 指示詞，好讓結果屬於 **xml** 類型。 如果未指定 `TYPE`，則結果會以 **nvarchar(max)** 類型傳回，而 XML 資料會以實體傳回。  
  
-   外部查詢也可以指定 `TYPE` 指示詞。 因此，此查詢的結果會以 **xml** 類型傳回給用戶端。  
  
 以下是部份結果：  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 以下查詢只是前述查詢的延伸模組。 它會顯示 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的完整產品階層。 這包括下列項目：  
  
-   產品類別目錄  
  
-   每個_類別目錄中的產品子類別目錄  
  
-   每個子類別目錄中的產品型號  
  
-   每個型號中的產品  
  
 以下查詢應該有助於了解 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫：  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName,  
               (SELECT ProductModel.ProductModelID,   
                       ProductModel.Name as ModelName,  
                       (SELECT ProductID, Name as ProductName, Color  
                        FROM   Production.Product  
                        WHERE  Product.ProductModelID =   
                               ProductModel.ProductModelID  
                        FOR XML AUTO, TYPE)  
                FROM   (SELECT distinct ProductModel.ProductModelID,   
                               ProductModel.Name  
                        FROM   Production.ProductModel,   
                               Production.Product  
                        WHERE  ProductModel.ProductModelID =   
                               Product.ProductModelID  
                        AND    Product.ProductSubCategoryID =   
                               ProductSubCategory.ProductSubCategoryID)   
                                  ProductModel  
                FOR XML AUTO, type  
               )  
        FROM Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 以下是部份結果：  
  
```  
<Production.ProductCategory ProductCategoryID="1" CategoryName="Bikes">  
  <Production.ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bikes</SubCategoryName>  
    <ProductModel ProductModelID="19" ModelName="Mountain-100">  
      <Production.Product ProductID="771"   
                ProductName="Mountain-100 Silver, 38" Color="Silver" />  
      <Production.Product ProductID="772"   
                ProductName="Mountain-100 Silver, 42" Color="Silver" />  
      <Production.Product ProductID="773"   
                ProductName="Mountain-100 Silver, 44" Color="Silver" />  
        …  
    </ProductModel>  
     …  
```  
  
 如果從產生產品子類別目錄的巢狀 `ELEMENTS` 查詢移除 `FOR XML` 指示詞，整個結果將為屬性中心。 然後您可以無套疊的方式撰寫此查詢 加入 `ELEMENTS` 會使 XML 一部份為屬性中心，一部份為元素中心。 此結果無法由單一層 FOR XML 查詢產生。  
  
## 另請參閱  
 [使用巢狀 FOR XML 查詢](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  