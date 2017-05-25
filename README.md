inlineSVG 「SVGでレーダーチャートを作ろう」
=======
インラインSVGとは？
------------
そもそもSVGとは？

Schalable Vecter Graphicsの略で、HTMLと同じマークアップ言語の一種です。

JPEGやPNGなどのビットマップ形式とは違い、SVG画像はベクター形式で  
画像が拡大縮小回転されて表示されても画質が落ちたりすることがありません。  

インラインSVGの使い方

canvasというHTHML５で追加されたビットマップ形式の画像を描画するための要素に  
似ていて、インラインSVGはベクター形式の画像を描画することができる要素です。  

<svg></svg>で画像を表示する場所を作り、その内側に画像を描画していきます。  
使える要素は以下の通りです。  

*circle（円）  
*polygon（多角形）  
*rect（四角形）  
*ellipse　（楕円）  
*line（線）  
*polyline　（連続直線）  
*text　（テキスト）  

それそれが属性を持っていて、描画パラメーターを使用することで描画していきます。  


レーダーチャートを作ってみる！
------------
今回、レーダーチャートを作るにあたり、使う要素は「polygon」「circle」です。

「polygon」は、「points」「fill」「stroke」の３つの属性を持っています。  
「points」は角となる座標をx,y座標をセットで指定します。  
「fill」は塗りつぶす色を指定することができます。  
「stroke」は線の色を指定することができます。  
例）`<polygon points="x,y x,y x,y x,y" fill="#000000" stroke="#ff00000"　/> //黒字の赤線で四角形を描画  `

「circle」は「fill」「stroke」「cx」「cy」「r」の５つの属性をもっています  
「fill」「stroke」はpolygonと同様です。  
「cx」は円の中心のx座標を指定します。 
「cy」は円の中心のy座標を指定します。  
「r」は円の半径を指定することができます。  
例）`<circle cx="x" cy="y" r="5" fill="#000000" stroke="#ff00000" /> //黒字の赤線で円を描写`

これらの要素を使って、まずチャートの土台の五角形を作っていきます。 

    <div class="svg_container">  <!-- このdivの中にレーダーチャートを作っていきます -->
      <svg class="graph_foundation">
      </svg>
    </div>

インラインSVGについて紹介した時に説明したとおり、<svg></svg>の間に画像を描画していきます。  
    <svg class="graph_foundation">
         <polygon points="150,0 300,125 235,300 65,300 0,125" />
        <polygon points="150,25 266.5,135 220.5,277.5 79.5,277.5 33.3,135" />
        <polygon points="150,55 243,140 206.5,255 93.5,255 56.6,140" />
        <polygon points="150,80 220,150 192,232.5 107.2,232.5 79.9,150" />
        <polygon points="150,110 196,155 178,210 122,210 103.2,155" />
    </svg>

上記の5つのpolygonでレーダーチャートの土台の五角形ができました。
次にもっとそれっぽく線の色や線の種類を変えていきます。

通常、divなどの要素に線の色を設定するときは、borderなどを使っていました。  
インラインSVGの場合は下記のように記述することで、装飾を加える事ができます。  

    .graph_foundation polygon:nth-of-type(even) {
      fill:none;
      stroke: #7ac5e9;
      stroke-width:1;
      stroke-dasharray:3;
     }

「fill」「stroke」の他に「stroke-width」で線の太さを設定することができます。  
「stroke-dasharray」は指定した幅で破線にすることができ、複数の数字を設定することもできます。

また、今回は使用していませんが、これらの他に「stroke-linecap」というプロパティで  
線端の形を変えることができます。  

作った土台の五角形の頂点からx,y座標セットを選んで、土台の五角形と同様に一番上の五角形を制作していきます。  
（フォームで入力した値をもとにステータス多角形を作れたらおもしろそう（添付のHTMLでピンクの多角形））  
また土台と同じようにCSSで装飾も加えましょう。  
<HTML>
    <polygon class="status" points="150,55 300,125 206.5,255 65,300 33.3,135"/>

<CSS>
    div.svg_container polygon.status{
      fill:#ff8e8e;
      stroke: none;
      filter:alpha(opacity=80);
      -moz-opacity: 0.8;
      opacity: 0.8;
     }

これでチャートの上に赤い五角形がのりました。  
この五角形のpointをjavascriptで取得して、それぞれの座標を使ってcircle要素  
を作成すると、赤い五角形の上に●点を置く事ができます。  
（サンプルのHTMLのscript内でsvg要素を作っています。が・・・上手く動いていない・・・・）  

同じ要領でレーダーチャートの内容を加えていきます。（未着手。エンジニアのスキルレーダーチャートとか・・・？）  

完成！
