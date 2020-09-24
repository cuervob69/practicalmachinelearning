
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># This R environment comes with many helpful analytics packages installed</span>
<span class="c1"># It is defined by the kaggle/rstats Docker image: https://github.com/kaggle/docker-rstats</span>
<span class="c1"># For example, here's a helpful package to load</span>

<span class="kn">library</span><span class="p">(</span>tidyverse<span class="p">)</span> <span class="c1"># metapackage of all tidyverse packages</span>

<span class="c1"># Input data files are available in the read-only "../input/" directory</span>
<span class="c1"># For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory</span>

<span class="kp">list.files</span><span class="p">(</span>path <span class="o">=</span> <span class="s">"../input"</span><span class="p">)</span>

<span class="c1"># You can write up to 5GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save &amp; Run All" </span>
<span class="c1"># You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Prediction Assignment Writeup</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Reading datasets</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Reading training dataset</span>
training <span class="o">&lt;-</span> read_csv <span class="p">(</span><span class="s">"../input/pmltestingcsv/pml-training.csv"</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Reading testing dataset</span>
testing <span class="o">&lt;-</span> read_csv <span class="p">(</span><span class="s">"../input/pmltestingcsv/pml-testing.csv"</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Loading package required</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Loading package required</span>
<span class="kn">library</span><span class="p">(</span>caret<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Converting datasets into Data Frames</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Converting training dataset into Data Frame</span>
as.data.frame <span class="p">(</span>training<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Converting testing dataset into Data Frame</span>
as.data.frame <span class="p">(</span>testing<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Tidying up datasets</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Checking for Na's in training dataset</span>
colSums <span class="p">(</span>is.na <span class="p">(</span>training<span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Checking for NA's in testing dataset</span>
colSums <span class="p">(</span>is.na <span class="p">(</span>testing<span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Removing NA's from training dataset</span>
training <span class="o">&lt;-</span> training <span class="p">[,</span> which <span class="p">(</span>colSums <span class="p">(</span>is.na <span class="p">(</span>training<span class="p">))</span> <span class="o">==</span> <span class="m">0</span><span class="p">)]</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>any <span class="p">(</span>is.na <span class="p">(</span>training<span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Removing NA's from testing dataset </span>
testing <span class="o">&lt;-</span> testing <span class="p">[,</span> which <span class="p">(</span>colSums <span class="p">(</span>is.na <span class="p">(</span>testing<span class="p">))</span> <span class="o">==</span> <span class="m">0</span><span class="p">)]</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>any <span class="p">(</span>is.na <span class="p">(</span>testing<span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Removing features not needed in training dataset</span>
training <span class="o">&lt;-</span> training <span class="p">[,</span> <span class="o">-</span><span class="p">(</span><span class="m">1</span><span class="o">:</span> <span class="m">7</span><span class="p">)]</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>dim <span class="p">(</span>training<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Removing features not needed in testing dataset</span>
testing <span class="o">&lt;-</span> testing <span class="p">[,</span> <span class="o">-</span><span class="p">(</span><span class="m">1</span><span class="o">:</span> <span class="m">7</span><span class="p">)]</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>dim <span class="p">(</span>testing<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Preprocessing datasets</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Checking for near-zero variance predictors in training dataset</span>
nzv <span class="o">&lt;-</span> nearZeroVar <span class="p">(</span>training<span class="p">,</span> saveMetrics<span class="o">=</span><span class="kc">TRUE</span><span class="p">)</span>
nzv
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Non near-zero variance predictors in training dataset.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Standardizing datasets</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Standardizing training dataset.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>summary <span class="p">(</span>training<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>preObj <span class="o">&lt;-</span> preProcess <span class="p">(</span>training<span class="p">,</span> <span class="kt">c</span><span class="p">(</span><span class="s">"center"</span><span class="p">,</span> <span class="s">"scale"</span><span class="p">))</span>
print <span class="p">(</span>preObj<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>training <span class="o">&lt;-</span> predict <span class="p">(</span>preObj<span class="p">,</span> training<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>summary <span class="p">(</span>training<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Standardizing testing dataset.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>summary <span class="p">(</span>testing<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>testing <span class="o">&lt;-</span> predict <span class="p">(</span>preObj<span class="p">,</span> testing<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>summary <span class="p">(</span>testing<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Splitting training dataset</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Splitting training dataset into train and validation sets</span>
seed <span class="o">&lt;-</span> <span class="m">18989</span>
set.seed <span class="p">(</span>seed<span class="p">)</span>
training <span class="o">=</span> <span class="kt">data.frame</span><span class="p">(</span>training<span class="p">)</span>
inTrain <span class="o">&lt;-</span> createDataPartition<span class="p">(</span>training<span class="o">$</span>classe<span class="p">,</span> p<span class="o">=</span><span class="m">0.70</span><span class="p">,</span> <span class="kt">list</span><span class="o">=</span><span class="kc">FALSE</span><span class="p">)</span>
train <span class="o">&lt;-</span> training<span class="p">[</span>inTrain<span class="p">,</span> <span class="p">]</span>
validation <span class="o">&lt;-</span> training<span class="p">[</span><span class="o">-</span>inTrain<span class="p">,</span> <span class="p">]</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Modeling</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Modeling with Linear Discriminant Analysis (LDA)</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Fitting LDA in train set</span>
set.seed <span class="p">(</span>seed<span class="p">)</span>
trainfitlda <span class="o">&lt;-</span> train <span class="p">(</span>classe<span class="o">~</span><span class="m">.</span><span class="p">,</span> method<span class="o">=</span><span class="s">"lda"</span><span class="p">,</span> data <span class="o">=</span> train<span class="p">)</span>
confusionMatrix <span class="p">(</span>trainfitlda<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Applying LDA train model fit in validation set</span>
vallda <span class="o">&lt;-</span> predict <span class="p">(</span>trainfitlda<span class="p">,</span> validation<span class="p">)</span>
confusionMatrix <span class="p">(</span>factor <span class="p">(</span>validation<span class="o">$</span>classe<span class="p">),</span> factor <span class="p">(</span>vallda<span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Modeling with Classification Tree (RPART)</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Fitting RPART in train set</span>
set.seed <span class="p">(</span>seed<span class="p">)</span>
trainfitrpart <span class="o">&lt;-</span> train <span class="p">(</span>classe <span class="o">~</span> <span class="m">.</span><span class="p">,</span> method<span class="o">=</span><span class="s">"rpart"</span><span class="p">,</span> data<span class="o">=</span>train<span class="p">)</span>
confusionMatrix <span class="p">(</span>trainfitrpart<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="c1"># Applying RPART train fit model in validation set</span>
valrpart <span class="o">&lt;-</span> predict <span class="p">(</span>trainfitrpart<span class="p">,</span> validation<span class="p">)</span>
confusionMatrix <span class="p">(</span>factor <span class="p">(</span>validation<span class="o">$</span>classe<span class="p">),</span> valrpart<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Modeling testing</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Predicting with LDA</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>testing <span class="o">&lt;-</span> predict <span class="p">(</span>trainfitlda<span class="p">,</span> testing<span class="p">)</span>
testing
</pre></div>

    </div>
</div>
</div>

</div>
    </div>
  </div>


 



