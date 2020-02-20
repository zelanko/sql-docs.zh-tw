---
title: 步驟 1:設定 Node.js 開發的開發環境 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce89cc12c7493522de55adffb69fcbe3307cbdf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68003756"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>步驟 1:設定 Node.js 開發的開發環境
您必須使用必要條件設定您的開發環境，才能使用 Node.js Driver for SQL Server 開發應用程式。  最常見的方法是使用節點套件管理員 (npm) 安裝 Tedious 模組，但是您可以視需要，直接在 [Github](https://github.com/pekim/tedious) 下載 Tedious 模組。  
  
請注意，Node.js 驅動程式會使用預設在 SQL Server 和 Azure SQL Database 中啟用的 TDS 通訊協定。  不需要進行其他組態設定。  
  
## <a name="windows"></a>Windows  
  
1. **安裝 Node.js 執行階段和 npm 套件管理員**  
a. 移至 [Node.js](https://nodejs.org/en/download/)  
b. 按一下適當的 Windows Installer msi 連結。   
c. 下載完成後，請執行 msi 以安裝 Node.js  
  
2. **開啟 cmd.exe**  
  
3. **建立專案目錄**並瀏覽到該目錄。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **建立節點專案。**  若要在專案建立期間保留預設值，請在建立專案之前按下 Enter 鍵。 在此步驟結束時，您應該會在您的專案目錄中看到一個 package.json 檔案。  
```  
> npm init  
```  
  
5. **在您的專案中安裝 Tedious 模組。**  這是驅動程式用來與 SQL Server 進行通訊之 TDS 通訊協定的實作。  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **開啟終端機**  
  
2. **安裝 Node.js 執行階段**  
```  
>sudo apt-get install node  
```  
3. **安裝 npm (節點套件管理員)**  
```  
> sudo apt-get install npm  
```  
4. **建立專案目錄**並瀏覽到該目錄。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **建立節點專案。**  若要在專案建立期間保留預設值，請在建立專案之前按下 Enter 鍵。 在此步驟結束時，您應該會在您的專案目錄中看到一個 package.json 檔案。  
```  
> sudo npm init  
```  
  
6. **在您的專案中安裝 Tedious 模組。**  這是驅動程式用來與 SQL Server 進行通訊之 TDS 通訊協定的實作。  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **安裝 Node.js 執行階段和 npm 套件管理員**  
a. 移至 [Node.js](https://nodejs.org/en/download/)  
b. 按一下適當的 Mac OS 安裝程式連結。  
c. 下載完成後，請執行 dmg 以安裝 Node.js  
  
2. **開啟終端機**  
  
3. **建立專案目錄**並瀏覽到該目錄。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **建立節點專案。**  若要在專案建立期間保留預設值，請在建立專案之前按下 Enter 鍵。 在此步驟結束時，您應該會在您的專案目錄中看到一個 package.json 檔案。  
```  
> npm init  
```  
  
5. **在您的專案中安裝 Tedious 模組。**  這是驅動程式用來與 SQL Server 進行通訊之 TDS 通訊協定的實作。  
```  
> npm install tedious  
```  
  
