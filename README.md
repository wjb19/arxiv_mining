# arxiv_mining
I've established this repos as a temporary resting place for data extracted from arxiv using the p2t API. At least initially, you should find a file called result.json, the results of applying the p2t bbox and simple-scatter-plot API methods to all pdf pages in the initial tar volume available for arxiv, arXiv_pdf_0001_001.tar

If you peek at these records, each element in the array gives some json describing:

i) the input document, specifically the arxiv URL (as per the policy found here : https://arxiv.org/help/bulk_data_s3)

ii) the page image that the result comes from,

iii) the JSON data file extracted from the region of the page, which corresponds to x-y values inverted from the scaling information found in the image

iv) the input bounding box region extracted from the page, and lastly

v) an image showing the fit produced by the simple-scatter-plot API method eg., the locations whose index value corresponds to the position of the corresponding x-y values in the output JSON.

One such element of result.json looks like: 

{
"url":"http://arxiv.org/abs/astro-ph/0001003",

"page":"outputs/astro-ph0001003-000005.png",

"data":"outputs/e154b55290bc2eea70f5a226806c2072.json",

"input":"outputs/e154b55290bc2eea70f5a226806c2072_in.png",

"fit":"outputs/e154b55290bc2eea70f5a226806c2072_out.png"
}


If you wanted to import this complete array into mongo DB (for example) , you could issue something like: 

mongoimport --db dbName --collection collectionName --file result.json --jsonArray

With a few tweaks, you could use the code of this repos to create a browser for the data: https://github.com/wjb19/basic_fig_search. 
Last but not least, a selection of the output images is available in the file arXiv_pdf_0001_001_text_out.tar.gz and the text extraction results are available in arXiv_pdf_0001_001_text_out.tar.gz. The entire dataset is too large for github, though rather small relatively; ~2500 figures modeled as simple scatter plots was extracted from ~ 1700 documents ie., in arxiv there approximately 1M such datasets available, given the time and computation. This set was produced in less than a day using single core / serial requests to the API.

So that you're not obliged to download the whole repos, I've placed a few preview images in src too. Note the simple-scatter-plot method doesn't try to filter non-data points as of yet, and scaling information will have some false positives / poor results in the presence of non-linear/log scales. 

WJB 01/18
