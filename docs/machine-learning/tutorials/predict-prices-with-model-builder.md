---
title: モデル ビルダーで回帰を使用して価格を予測する
description: このチュートリアルでは、ML.NET モデル ビルダーを使用して、価格 (具体的にはニューヨーク市のタクシー運賃) を予測する回帰モデルを構築する方法を示します。
author: luisquintanilla
ms.author: luquinta
ms.date: 07/15/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: b4a08a9866bbc8816b57c95bdb22766bd1b07fdc
ms.sourcegitcommit: 09d699aca28ae9723399bbd9d3d44aa0cbd3848d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68331700"
---
# <a name="predict-prices-using-regression-with-model-builder"></a><span data-ttu-id="69ad5-103">モデル ビルダーで回帰を使用して価格を予測する</span><span class="sxs-lookup"><span data-stu-id="69ad5-103">Predict prices using regression with Model Builder</span></span>

<span data-ttu-id="69ad5-104">ML.NET モデル ビルダーを使用して、価格を予測する回帰モデル () を構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-104">Learn how to use ML.NET Model Builder to build a regression model() to predict prices.</span></span>  <span data-ttu-id="69ad5-105">このチュートリアルで開発する .NET コンソール アプリでは、過去のニューヨーク市のタクシー運賃データに基づいてタクシー運賃を予測します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-105">The .NET console app that you develop in this tutorial predicts taxi fares based on historical New York taxi fare data.</span></span>

<span data-ttu-id="69ad5-106">モデル ビルダーの価格予測テンプレートは、数値による予測値を必要とするすべてのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-106">The Model Builder price prediction template can be used for any scenario requiring a numerical prediction value.</span></span> <span data-ttu-id="69ad5-107">シナリオの例には、住宅価格の予測、需要予測、売上予測などがあります。</span><span class="sxs-lookup"><span data-stu-id="69ad5-107">Example scenarios include: house price prediction, demand prediction, and sales forecasting.</span></span>

<span data-ttu-id="69ad5-108">このチュートリアルでは、次の作業を行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-108">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="69ad5-109">データを準備して理解する</span><span class="sxs-lookup"><span data-stu-id="69ad5-109">Prepare and understand the data</span></span>
> * <span data-ttu-id="69ad5-110">シナリオを選択する</span><span class="sxs-lookup"><span data-stu-id="69ad5-110">Choose a scenario</span></span>
> * <span data-ttu-id="69ad5-111">データを読み込む</span><span class="sxs-lookup"><span data-stu-id="69ad5-111">Load the data</span></span>
> * <span data-ttu-id="69ad5-112">モデルをトレーニングする</span><span class="sxs-lookup"><span data-stu-id="69ad5-112">Train the model</span></span>
> * <span data-ttu-id="69ad5-113">モデルを評価する</span><span class="sxs-lookup"><span data-stu-id="69ad5-113">Evaluate the model</span></span>
> * <span data-ttu-id="69ad5-114">モデルを使用して予測を行う</span><span class="sxs-lookup"><span data-stu-id="69ad5-114">Use the model for predictions</span></span>

> [!NOTE]
> <span data-ttu-id="69ad5-115">モデル ビルダーは現在のところ、プレビュー段階です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-115">Model Builder is currently in Preview.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="69ad5-116">前提条件</span><span class="sxs-lookup"><span data-stu-id="69ad5-116">Pre-requisites</span></span>

<span data-ttu-id="69ad5-117">前提条件の一覧とインストール手順は、[モデル ビルダーのインストール ガイド](../how-to-guides/install-model-builder.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="69ad5-117">For a list of pre-requisites and installation instructions, visit the [Model Builder installation guide](../how-to-guides/install-model-builder.md).</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="69ad5-118">コンソール アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="69ad5-118">Create a console application</span></span>

1. <span data-ttu-id="69ad5-119">"TaxiFarePrediction" という名前の **.NET Core コンソール アプリケーション**を作成します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-119">Create a **.NET Core Console Application** called "TaxiFarePrediction".</span></span>

## <a name="prepare-and-understand-the-data"></a><span data-ttu-id="69ad5-120">データを準備して理解する</span><span class="sxs-lookup"><span data-stu-id="69ad5-120">Prepare and understand the data</span></span>

1. <span data-ttu-id="69ad5-121">プロジェクトに *Data* という名前のディレクトリを作成して、データ セットのファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-121">Create a directory named *Data* in your project to store the data set files.</span></span>

1. <span data-ttu-id="69ad5-122">機械学習モデルのトレーニングと評価に使用するデータ セットは、NYC TLC Taxi Trip データ セットから取得したものです。</span><span class="sxs-lookup"><span data-stu-id="69ad5-122">The data set used to train and evaluate the machine learning model is originally from the NYC TLC Taxi Trip data set.</span></span>

    <span data-ttu-id="69ad5-123">このデータ セットをダウンロードするには、[taxi-fare-train.csv のダウンロード リンク](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/taxi-fare-train.csv)に移動します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-123">To download the data set, navigate to the [taxi-fare-train.csv download link](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/taxi-fare-train.csv).</span></span>

    <span data-ttu-id="69ad5-124">ページが読み込まれたら、ページ上の任意の場所を右クリックして、 **[名前を付けて保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-124">When the page loads, right-click anywhere on the page and select **Save as**.</span></span>

    <span data-ttu-id="69ad5-125">**[名前を付けて保存] ダイアログ**を使って、前の手順で作成した *Data* フォルダーにファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-125">Use the **Save As Dialog** to save the file in the *Data* folder you created at the previous step.</span></span>

1. <span data-ttu-id="69ad5-126">**ソリューション エクスプローラー**で、 *[taxi-fare-train.csv]* ファイルを右クリックし、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-126">In **Solution Explorer**, right-click the *taxi-fare-train.csv* file and select **Properties**.</span></span> <span data-ttu-id="69ad5-127">**[詳細設定]** で、 **[出力ディレクトリにコピー]** の値を **[新しい場合はコピーする]** に変更します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-127">Under **Advanced**, change the value of **Copy to Output Directory** to **Copy if newer**.</span></span>

<span data-ttu-id="69ad5-128">`taxi-fare-train.csv` データ セットの各行に、タクシーの移動の詳細が含まれています。</span><span class="sxs-lookup"><span data-stu-id="69ad5-128">Each row in the `taxi-fare-train.csv` data set contains details of trips made by a taxi.</span></span>

1. <span data-ttu-id="69ad5-129">**taxi-fare-train.csv** データ セットを開きます</span><span class="sxs-lookup"><span data-stu-id="69ad5-129">Open the **taxi-fare-train.csv** data set</span></span>

    <span data-ttu-id="69ad5-130">提供されているデータ セットには、次の列が含まれます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-130">The provided data set contains the following columns:</span></span>

    * <span data-ttu-id="69ad5-131">**vendor_id:** タクシー会社の ID は特徴です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-131">**vendor_id:** The ID of the taxi vendor is a feature.</span></span>
    * <span data-ttu-id="69ad5-132">**rate_code:** タクシー旅行のレートの種類は特徴です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-132">**rate_code:** The rate type of the taxi trip is a feature.</span></span>
    * <span data-ttu-id="69ad5-133">**passenger_count:** 旅行の乗客数は特徴です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-133">**passenger_count:** The number of passengers on the trip is a feature.</span></span>
    * <span data-ttu-id="69ad5-134">**trip_time_in_secs:** 旅行の所要時間です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-134">**trip_time_in_secs:** The amount of time the trip took.</span></span>
    * <span data-ttu-id="69ad5-135">**trip_distance:** 旅行距離は特徴です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-135">**trip_distance:** The distance of the trip is a feature.</span></span>
    * <span data-ttu-id="69ad5-136">**payment_type:** 支払い方法 (現金またはクレジット カード) は特徴です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-136">**payment_type:** The payment method (cash or credit card) is a feature.</span></span>
    * <span data-ttu-id="69ad5-137">**fare_amount:** 支払った合計タクシー運賃はラベルです。</span><span class="sxs-lookup"><span data-stu-id="69ad5-137">**fare_amount:** The total taxi fare paid is the label.</span></span>

<span data-ttu-id="69ad5-138">`label` は予測する列です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-138">The `label` is the column you want to predict.</span></span> <span data-ttu-id="69ad5-139">回帰タスクを実行する場合の目標は、数値を予測することです。</span><span class="sxs-lookup"><span data-stu-id="69ad5-139">When performing a regression task, the goal is to predict a numerical value.</span></span> <span data-ttu-id="69ad5-140">この価格予測シナリオでは、タクシーの乗車のコストが予測されています。</span><span class="sxs-lookup"><span data-stu-id="69ad5-140">In this price prediction scenario, the cost of a taxi ride is being predicted.</span></span> <span data-ttu-id="69ad5-141">したがって、**fare_amount** がラベルです。</span><span class="sxs-lookup"><span data-stu-id="69ad5-141">Therefore, the **fare_amount** is the label.</span></span> <span data-ttu-id="69ad5-142">識別された `features` は、`label` を予測するためにモデルを指定する入力です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-142">The identified `features` are the inputs you give the model to predict the `label`.</span></span> <span data-ttu-id="69ad5-143">この場合、残りの列は、運賃の金額を予測するための機能または入力として使用されます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-143">In this case, the rest of the columns are used as features or inputs to predict the fare amount.</span></span>

## <a name="choose-a-scenario"></a><span data-ttu-id="69ad5-144">シナリオを選択する</span><span class="sxs-lookup"><span data-stu-id="69ad5-144">Choose a scenario</span></span>

<span data-ttu-id="69ad5-145">モデルをトレーニングするには、モデル ビルダーによって提供される機械学習シナリオの一覧から選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="69ad5-145">To train your model, you need to select from the list of available machine learning scenarios provided by Model Builder.</span></span> <span data-ttu-id="69ad5-146">この場合、シナリオは `Price Prediction` です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-146">In this case, the scenario is `Price Prediction`.</span></span>

1. <span data-ttu-id="69ad5-147">**ソリューション エクスプローラー**で、 *[TaxiFarePrediction]* プロジェクトを右クリックし、 **[追加]**  >  **[機械学習]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-147">In **Solution Explorer**, right-click the *TaxiFarePrediction* project, and select **Add** > **Machine Learning**.</span></span>
1. <span data-ttu-id="69ad5-148">モデル ビルダー ツールのシナリオの手順で、*価格の予測*のシナリオを選択します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-148">In the scenario step of the Model Builder tool, select *Price Prediction* scenario.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="69ad5-149">データを読み込む</span><span class="sxs-lookup"><span data-stu-id="69ad5-149">Load the data</span></span>

<span data-ttu-id="69ad5-150">モデル ビルダーは、SQL Server データベースか、csv または tsv 形式のローカル ファイルという 2 つのソースからデータを受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-150">Model Builder accepts data from two sources, a SQL Server database or a local file in csv or tsv format.</span></span>

1. <span data-ttu-id="69ad5-151">モデル ビルダー ツールのデータの手順で、データ ソースのドロップダウンから *[ファイル]* を選択します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-151">In the data step of the Model Builder tool, select *File* from the data source dropdown.</span></span>
1. <span data-ttu-id="69ad5-152">*[ファイルの選択]* テキスト ボックスの横にあるボタンを選択し、ファイル エクスプローラーを使用して *Data* ディレクトリにある *[taxi-fare-test.csv]* を参照し、選択します</span><span class="sxs-lookup"><span data-stu-id="69ad5-152">Select the button next to the *Select a file* text box and use File Explorer to browse and select the *taxi-fare-test.csv* in the *Data* directory</span></span>
1. <span data-ttu-id="69ad5-153">*[Label or Column to Predict]\(予測するラベルまたは列\)* ドロップダウンにある *[fare_amount]* を選択して、モデル ビルダー ツールのトレーニングの手順に移動します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-153">Choose *fare_amount* in the *Label or Column to Predict* dropdown and navigate to the train step of the Model Builder tool.</span></span>

## <a name="train-the-model"></a><span data-ttu-id="69ad5-154">モデルをトレーニングする</span><span class="sxs-lookup"><span data-stu-id="69ad5-154">Train the model</span></span>

<span data-ttu-id="69ad5-155">このチュートリアルで、価格予測モデルのトレーニングに使用する機械学習のタスクは、回帰です。</span><span class="sxs-lookup"><span data-stu-id="69ad5-155">The machine learning task used to train the price prediction model in this tutorial is regression.</span></span> <span data-ttu-id="69ad5-156">モデルのトレーニング プロセス中、モデル ビルダーは、さまざまな回帰アルゴリズムと設定を使用して、データセットで最も良いパフォーマンスのモデルを見つける個別のモデルをトレーニングします。</span><span class="sxs-lookup"><span data-stu-id="69ad5-156">During the model training process, Model Builder trains separate models using different regression algorithms and settings to find the best performing model for your dataset.</span></span>

<span data-ttu-id="69ad5-157">モデルのトレーニングに必要な時間は、データの量に比例します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-157">The time required for the model to train is proportionate to the amount of data.</span></span> <span data-ttu-id="69ad5-158">このグラフをガイダンスとして使用して、`Time to train (seconds)` フィールドに適した値を選択してください。</span><span class="sxs-lookup"><span data-stu-id="69ad5-158">Use this chart as guidance to select an adequate value for the `Time to train (seconds)` field:</span></span>

<span data-ttu-id="69ad5-159">\*データセットのサイズ</span><span class="sxs-lookup"><span data-stu-id="69ad5-159">\*Dataset Size</span></span>  | <span data-ttu-id="69ad5-160">データセットの種類</span><span class="sxs-lookup"><span data-stu-id="69ad5-160">Dataset Type</span></span>       | <span data-ttu-id="69ad5-161">Avg.トレーニング時間\*</span><span class="sxs-lookup"><span data-stu-id="69ad5-161">Avg. Time to train\*</span></span>
------------- | ------------------ | --------------
<span data-ttu-id="69ad5-162">0 - 10 Mb</span><span class="sxs-lookup"><span data-stu-id="69ad5-162">0 - 10 Mb</span></span>     | <span data-ttu-id="69ad5-163">数値とテキスト</span><span class="sxs-lookup"><span data-stu-id="69ad5-163">Numeric and Text</span></span>   | <span data-ttu-id="69ad5-164">10 秒</span><span class="sxs-lookup"><span data-stu-id="69ad5-164">10 sec</span></span>
<span data-ttu-id="69ad5-165">10 - 100 Mb</span><span class="sxs-lookup"><span data-stu-id="69ad5-165">10 - 100 Mb</span></span>   | <span data-ttu-id="69ad5-166">数値とテキスト</span><span class="sxs-lookup"><span data-stu-id="69ad5-166">Numeric and Text</span></span>   | <span data-ttu-id="69ad5-167">10 分</span><span class="sxs-lookup"><span data-stu-id="69ad5-167">10 min</span></span>
<span data-ttu-id="69ad5-168">100 - 500 Mb</span><span class="sxs-lookup"><span data-stu-id="69ad5-168">100 - 500 Mb</span></span>  | <span data-ttu-id="69ad5-169">数値とテキスト</span><span class="sxs-lookup"><span data-stu-id="69ad5-169">Numeric and Text</span></span>   | <span data-ttu-id="69ad5-170">30 分</span><span class="sxs-lookup"><span data-stu-id="69ad5-170">30 min</span></span>
<span data-ttu-id="69ad5-171">500 - 1 Gb</span><span class="sxs-lookup"><span data-stu-id="69ad5-171">500 - 1 Gb</span></span>    | <span data-ttu-id="69ad5-172">数値とテキスト</span><span class="sxs-lookup"><span data-stu-id="69ad5-172">Numeric and Text</span></span>   | <span data-ttu-id="69ad5-173">60 分</span><span class="sxs-lookup"><span data-stu-id="69ad5-173">60 min</span></span>
<span data-ttu-id="69ad5-174">1 Gb 超</span><span class="sxs-lookup"><span data-stu-id="69ad5-174">1 Gb+</span></span>         | <span data-ttu-id="69ad5-175">数値とテキスト</span><span class="sxs-lookup"><span data-stu-id="69ad5-175">Numeric and Text</span></span>   | <span data-ttu-id="69ad5-176">3 時間超</span><span class="sxs-lookup"><span data-stu-id="69ad5-176">3 hour+</span></span>

1. <span data-ttu-id="69ad5-177">トレーニング データ ファイルが 10 MB を超えているため、 *[Time to train (seconds)]\(トレーニング時間 (秒)\)* の値には 600 秒 (10 分) を使用してください。</span><span class="sxs-lookup"><span data-stu-id="69ad5-177">Because the training data file is more than 10MB, use 600 seconds (10 minutes) as the value for *Time to train (seconds)*.</span></span>
2. <span data-ttu-id="69ad5-178">*[Start Training]\(トレーニング開始\)* を選択します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-178">Select *Start Training*.</span></span>

<span data-ttu-id="69ad5-179">トレーニング プロセスを通して、進捗データがトレーニングの手順の `Progress` セクションに表示されます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-179">Throughout the training process, progress data is displayed in the `Progress` section of the train step.</span></span>

- <span data-ttu-id="69ad5-180">状態には、トレーニング プロセスの完了ステータスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-180">Status displays the completion status of the training process.</span></span>
- <span data-ttu-id="69ad5-181">[Best accuracy]\(最良の精度\) には、これまでにモデル ビルダーで見つかった最良のパフォーマンスのモデルの精度が表示されます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-181">Best accuracy displays the accuracy of the best performing model found by Model Builder so far.</span></span> <span data-ttu-id="69ad5-182">精度が高くなるほど、テスト データでモデルが正確に予測されたことになります。</span><span class="sxs-lookup"><span data-stu-id="69ad5-182">Higher accuracy means the model predicted more correctly on test data.</span></span>
- <span data-ttu-id="69ad5-183">[Best algorithm]\(最良のアルゴリズム\) には、これまでにモデル ビルダーで見つかった最良のパフォーマンスのアルゴリズムの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-183">Best algorithm displays the name of the best performing algorithm performed found by Model Builder so far.</span></span>
- <span data-ttu-id="69ad5-184">[Last algorithm]\(最後のアルゴリズム\) には、モデル ビルダーがモデルのトレーニングに最近使用したアルゴリズムの名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-184">Last algorithm displays the name of the algorithm most recently used by Model Builder to train the model.</span></span>

<span data-ttu-id="69ad5-185">トレーニングが完了したら、評価の手順に移動します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-185">Once training is complete, navigate to the evaluate step.</span></span>

## <a name="evaluate-the-model"></a><span data-ttu-id="69ad5-186">モデルを評価する</span><span class="sxs-lookup"><span data-stu-id="69ad5-186">Evaluate the model</span></span>

<span data-ttu-id="69ad5-187">トレーニングの手順の結果が、最良のパフォーマンスだった 1 つのモデルになります。</span><span class="sxs-lookup"><span data-stu-id="69ad5-187">The result of the training step will be one model which had the best performance.</span></span> <span data-ttu-id="69ad5-188">モデル ビルダー ツールの評価の手順の出力セクションには、 *[Best Model]\(最良のモデル\)* エントリの最良のパフォーマンスのモデルで使用されたアルゴリズムと、 *[Best Model Quality (RSquared)]\(最良のモデル品質 (RSquared)\)* のメトリックが含まれます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-188">In the evaluate step of the Model Builder tool, the output section, will contain the algorithm used by the best performing model in the *Best Model* entry along with metrics in *Best Model Quality (RSquared)*.</span></span> <span data-ttu-id="69ad5-189">また、概要テーブルには上位 5 つのモデルとそのメトリックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="69ad5-189">Additionally, a summary table containing top five models and their metrics.</span></span>

<span data-ttu-id="69ad5-190">精度のメトリックに不満がある場合、モデルのトレーニング時間を増やすか、さらに多くのデータを使用すると、モデルの精度を簡単に高めることができます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-190">If you're not satisfied with your accuracy metrics, some easy ways to try and improve model accuracy are to increase the amount of time to train the model or use more data.</span></span> <span data-ttu-id="69ad5-191">そうでない場合は、コードの手順に移動します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-191">Otherwise, navigate to the code step.</span></span>

## <a name="add-the-code-to-make-predictions"></a><span data-ttu-id="69ad5-192">予測を行うコードを追加する</span><span class="sxs-lookup"><span data-stu-id="69ad5-192">Add the code to make predictions</span></span>

<span data-ttu-id="69ad5-193">トレーニング プロセスの結果として 2 つのプロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-193">Two projects will be created as a result of the training process.</span></span>

- <span data-ttu-id="69ad5-194">TaxiFarePredictionML.ConsoleApp: モデルのトレーニングと使用に関するコードが含まれる .NET Core コンソール アプリケーション。</span><span class="sxs-lookup"><span data-stu-id="69ad5-194">TaxiFarePredictionML.ConsoleApp: A .NET Core Console application that contains the model training and consumption code.</span></span>
- <span data-ttu-id="69ad5-195">TaxiFarePredictionML.Model: 入出力モデル データのスキーマを定義するデータ モデルと、トレーニング中にパフォーマンスが最も良かったモデルの永続化バージョンが含まれる .NET Standard クラス ライブラリ。</span><span class="sxs-lookup"><span data-stu-id="69ad5-195">TaxiFarePredictionML.Model: A .NET Standard class library containing the data models that define the schema of input and output model data as well as the persisted version of the best performing model during training.</span></span>

1. <span data-ttu-id="69ad5-196">モデル ビルダー ツールのコードの手順で、 **[プロジェクトの追加]** を選択して、自動生成されたプロジェクトをソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-196">In the code step of the Model Builder tool, select **Add Projects** to add the auto-generated projects to the solution.</span></span>
1. <span data-ttu-id="69ad5-197">*[TaxiFarePrediction]* プロジェクトを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="69ad5-197">Right-click *TaxiFarePrediction* project.</span></span> <span data-ttu-id="69ad5-198">それから、 **[追加]、[参照]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-198">Then, **Add > Reference**.</span></span> <span data-ttu-id="69ad5-199">**[プロジェクト]、[ソリューション]** ノードを選択し、一覧で *[TaxiFarePredictionML.Model]* プロジェクトを選択して [OK] を選択します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-199">Choose the **Projects > Solution** node and from the list, check the *TaxiFarePredictionML.Model* project and select OK.</span></span>
1. <span data-ttu-id="69ad5-200">*[TaxiFarePrediction]* プロジェクトの *[Program.cs]* ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-200">Open the *Program.cs* file in the *TaxiFarePrediction* project.</span></span>
1. <span data-ttu-id="69ad5-201">*Microsoft.ML* NuGet パッケージと *TaxiFarePredictionML.Model* プロジェクトを参照するために、次の using ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-201">Add the following using statements to reference the *Microsoft.ML* NuGet package and *TaxiFarePredictionML.Model* project:</span></span>

    ```csharp
    using System;
    using Microsoft.ML;
    using TaxiFarePredictionML.Model.DataModels;
    ```

1. <span data-ttu-id="69ad5-202">`ConsumeModel` メソッドを `Program` クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-202">Add the `ConsumeModel` method to the `Program` class.</span></span>

    ```csharp
    static ModelOutput ConsumeModel(ModelInput input)
    {
        // 1. Load the model
        MLContext mlContext = new MLContext();
        ITransformer mlModel = mlContext.Model.Load("MLModel.zip", out var modelInputSchema);

        // 2. Create PredictionEngine
        var predictionEngine = mlContext.Model.CreatePredictionEngine<ModelInput, ModelOutput>(mlModel);

        // 3. Use PredictionEngine to use model on input data
        ModelOutput result = predictionEngine.Predict(input);

        // 4. Return prediction result
        return result;
    }
    ```

    <span data-ttu-id="69ad5-203">`ConsumeModel` によって、トレーニング済みのモデルが読み込まれ、モデル用の [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) が作成され、それを使った予測が新しいデータで実行されます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-203">The `ConsumeModel` will load the trained model, create a [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) for the model and use it to make predictions on new data.</span></span>

1. <span data-ttu-id="69ad5-204">新しいデータに対してモデルを使った予測を行うには、`ModelInput` クラスの新しいインスタンスを作成し、`ConsumeModel` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="69ad5-204">To make a prediction on new data using the model, create a new instance of the `ModelInput` class and use the `ConsumeModel` method.</span></span> <span data-ttu-id="69ad5-205">運賃額が入力に含まれていないことがわかります。</span><span class="sxs-lookup"><span data-stu-id="69ad5-205">Notice that the fare amount is not part of the input.</span></span> <span data-ttu-id="69ad5-206">これは、モデルによってその予測が生成されるためです。</span><span class="sxs-lookup"><span data-stu-id="69ad5-206">This is because the model will generate the prediction for it.</span></span> <span data-ttu-id="69ad5-207">`Main` メソッドに次のコードを追加して、アプリケーションを実行します</span><span class="sxs-lookup"><span data-stu-id="69ad5-207">Add the following code to the `Main` method and run the application</span></span>

    ```csharp
    // Create sample data
    ModelInput input = new ModelInput()
    {
        Vendor_id = "CMT",
        Rate_code = 1,
        Passenger_count = 1,
        Trip_time_in_secs = 1271,
        Trip_distance = 3.8f,
        Payment_type = "CRD"
    };

    // Make prediction
    ModelOutput prediction = ConsumeModel(input);

    // Print Prediction
    Console.WriteLine($"Predicted Fare: {prediction.Score}");
    Console.ReadKey();
    ```

    <span data-ttu-id="69ad5-208">プログラムによって生成される出力は次のスニペットのようになります。</span><span class="sxs-lookup"><span data-stu-id="69ad5-208">The output generated by the program should look similar to the snippet below:</span></span>

    ```bash
    Predicted Fare: 16.82245
    ```

<span data-ttu-id="69ad5-209">別のソリューション内で後で生成されたプロジェクトを参照する必要がある場合は、`C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` ディレクトリを検索することができます。</span><span class="sxs-lookup"><span data-stu-id="69ad5-209">If you need to reference the generated projects at a later time inside of another solution, you can find them inside the `C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69ad5-210">次の手順</span><span class="sxs-lookup"><span data-stu-id="69ad5-210">Next Steps</span></span>

<span data-ttu-id="69ad5-211">このチュートリアルでは、次の作業を行う方法を学びました。</span><span class="sxs-lookup"><span data-stu-id="69ad5-211">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="69ad5-212">データを準備して理解する</span><span class="sxs-lookup"><span data-stu-id="69ad5-212">Prepare and understand the data</span></span>
> * <span data-ttu-id="69ad5-213">シナリオを選択する</span><span class="sxs-lookup"><span data-stu-id="69ad5-213">Choose a scenario</span></span>
> * <span data-ttu-id="69ad5-214">データを読み込む</span><span class="sxs-lookup"><span data-stu-id="69ad5-214">Load the data</span></span>
> * <span data-ttu-id="69ad5-215">モデルをトレーニングする</span><span class="sxs-lookup"><span data-stu-id="69ad5-215">Train the model</span></span>
> * <span data-ttu-id="69ad5-216">モデルを評価する</span><span class="sxs-lookup"><span data-stu-id="69ad5-216">Evaluate the model</span></span>
> * <span data-ttu-id="69ad5-217">モデルを使用して予測を行う</span><span class="sxs-lookup"><span data-stu-id="69ad5-217">Use the model for predictions</span></span>

### <a name="additional-resources"></a><span data-ttu-id="69ad5-218">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="69ad5-218">Additional Resources</span></span>

<span data-ttu-id="69ad5-219">このチュートリアルで説明しているトピックについて詳しくは、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="69ad5-219">To learn more about topics mentioned in this tutorial, visit the following resources:</span></span>

- [<span data-ttu-id="69ad5-220">モデル ビルダーのシナリオ</span><span class="sxs-lookup"><span data-stu-id="69ad5-220">Model Builder Scenarios</span></span>](../automate-training-with-model-builder.md#scenarios)
- [<span data-ttu-id="69ad5-221">モデル ビルダーのデータ形式</span><span class="sxs-lookup"><span data-stu-id="69ad5-221">Model Builder Data Formats</span></span>](../automate-training-with-model-builder.md#data-formats)
- [<span data-ttu-id="69ad5-222">回帰</span><span class="sxs-lookup"><span data-stu-id="69ad5-222">Regression</span></span>](../resources/glossary.md#regression)
- [<span data-ttu-id="69ad5-223">回帰モデルのメトリック</span><span class="sxs-lookup"><span data-stu-id="69ad5-223">Regression Model Metrics</span></span>](../resources/metrics.md#metrics-for-regression)
- [<span data-ttu-id="69ad5-224">NYC TLC Taxi Trip データ セット</span><span class="sxs-lookup"><span data-stu-id="69ad5-224">NYC TLC Taxi Trip data set</span></span>](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)