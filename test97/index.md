---
title: チュートリアル:Azure portal を使用して Azure Firewall のデプロイと構成を行う
description: このチュートリアルでは、Azure portal を使用して Azure Firewall をデプロイおよび構成する方法を学習します。
services: firewall
author: vhorne
ms.service: firewall
ms.topic: tutorial
ms.date: 10/28/2019
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: be39449c1c11acdbdc99bd96f917c51eebda44ae
ms.sourcegitcommit: 8e31a82c6da2ee8dafa58ea58ca4a7dd3ceb6132
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74195789"
---
<span data-ttu-id="b5323-122">このチュートリアルでは、以下の内容を学習します。</span><span class="sxs-lookup"><span data-stu-id="b5323-122">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5323-123">テスト ネットワーク環境を設定する</span><span class="sxs-lookup"><span data-stu-id="b5323-123">Set up a test network environment</span></span>
> * <span data-ttu-id="b5323-124">ファイアウォールをデプロイする</span><span class="sxs-lookup"><span data-stu-id="b5323-124">Deploy a firewall</span></span>
> * <span data-ttu-id="b5323-125">既定のルートを作成する</span><span class="sxs-lookup"><span data-stu-id="b5323-125">Create a default route</span></span>
> * <span data-ttu-id="b5323-126">www.google.com へのアクセスを許可するようにアプリケーションを構成する</span><span class="sxs-lookup"><span data-stu-id="b5323-126">Configure an application rule to allow access to www.google.com</span></span>
> * <span data-ttu-id="b5323-127">外部 DNS サーバーへのアクセスを許可するようにネットワーク ルールを構成する</span><span class="sxs-lookup"><span data-stu-id="b5323-127">Configure a network rule to allow access to external DNS servers</span></span>
> * <span data-ttu-id="b5323-128">ファイアウォールをテストする</span><span class="sxs-lookup"><span data-stu-id="b5323-128">Test the firewall</span></span>

<span data-ttu-id="b5323-122">このチュートリアルでは、以下の内容を学習します。</span><span class="sxs-lookup"><span data-stu-id="b5323-122">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5323-123">テスト ネットワーク環境を設定する</span><span class="sxs-lookup"><span data-stu-id="b5323-123">Set up a test network environment</span></span>
> * <span data-ttu-id="b5323-124">ファイアウォールをデプロイする</span><span class="sxs-lookup"><span data-stu-id="b5323-124">Deploy a firewall</span></span>
> * <span data-ttu-id="b5323-125">既定のルートを作成する</span><span class="sxs-lookup"><span data-stu-id="b5323-125">Create a default route</span></span>
> * <span data-ttu-id="b5323-126"> www.google.com へのアクセスを許可するようにアプリケーションを構成する</span><span class="sxs-lookup"><span data-stu-id="b5323-126">Configure an application rule to allow access to www.google.com</span></span>
> * <span data-ttu-id="b5323-127">外部 DNS サーバーへのアクセスを許可するようにネットワーク ルールを構成する</span><span class="sxs-lookup"><span data-stu-id="b5323-127">Configure a network rule to allow access to external DNS servers</span></span>
> * <span data-ttu-id="b5323-128">ファイアウォールをテストする</span><span class="sxs-lookup"><span data-stu-id="b5323-128">Test the firewall</span></span>
<span data-ttu-id="b5323-122">このチュートリアルでは、以下の内容を学習します。</span><span class="sxs-lookup"><span data-stu-id="b5323-122">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5323-123">テスト ネットワーク環境を設定する</span><span class="sxs-lookup"><span data-stu-id="b5323-123">Set up a test network environment</span></span>
> * <span data-ttu-id="b5323-124">ファイアウォールをデプロイする</span><span class="sxs-lookup"><span data-stu-id="b5323-124">Deploy a firewall</span></span>
> * <span data-ttu-id="b5323-125">既定のルートを作成する</span><span class="sxs-lookup"><span data-stu-id="b5323-125">Create a default route</span></span>
> * <span data-ttu-id="b5323-126">http:\\portal.azure.com へのアクセスを許可するようにアプリケーションを構成する</span><span class="sxs-lookup"><span data-stu-id="b5323-126">Configure an application rule to allow access to www.google.com</span></span>
> * <span data-ttu-id="b5323-127">外部 DNS サーバーへのアクセスを許可するようにネットワーク ルールを構成する</span><span class="sxs-lookup"><span data-stu-id="b5323-127">Configure a network rule to allow access to external DNS servers</span></span>
> * <span data-ttu-id="b5323-128">ファイアウォールをテストする</span><span class="sxs-lookup"><span data-stu-id="b5323-128">Test the firewall</span></span>
> * <span data-ttu-id="b5323-126"> http:\\portal.azure.com へのアクセスを許可するようにアプリケーションを構成する</span><span class="sxs-lookup"><span data-stu-id="b5323-126">Configure an application rule to allow access to www.google.com</span></span>
> * <span data-ttu-id="b5323-127">外部 DNS サーバーへのアクセスを許可するようにネットワーク ルールを構成する</span><span class="sxs-lookup"><span data-stu-id="b5323-127">Configure a network rule to allow access to external DNS servers</span></span>
> * <span data-ttu-id="b5323-128">ファイアウォールをテストする</span><span class="sxs-lookup"><span data-stu-id="b5323-128">Test the firewall</span></span>
