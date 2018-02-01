# Windows コマンドプロンプトで kozos on zero-riscy を動かす
### このリポジトリに含まれるもの
- kozos のソース
- zero-riscy シミュレータの実行ファイル

### このリポジトリに含まれないもの
- zero-riscy シミュレータのソース
- zero-riscy コアのソース
- RISC-V ソフト開発環境
- make

このシステムは割り込み発生機能を持たないので、kozos 本の Step6 までを実装しています。
## 準備
### RISC-V ソフト開発環境のインストール
[SiFive の開発ツールの HP](https://www.sifive.com/products/tools/) から ```SiFive GNU Embedded Toolchain v20171231 Windows``` をダウンロードして、適当なディレクトリに展開する。  
このリポジトリは ```${HOME}\bin\riscv64-unknown-elf-gcc-20171231-x86_64-w64-mingw32``` を前提としている。

### make のインストール
自分の使い慣れた make を持っているならそれを使うと良いです。  
ないなら、 [GnuWin の make の HP](http://gnuwin32.sourceforge.net/packages/make.htm) から ```Complete package, except sources``` をダウンロード。ちょっとバージョンが古いですが…  
後は、ダウンロードしたインストーラを実行するだけ。

## kozos のコンパイル
自分で準備した make を使うときは適宜読み替える。

```
cd ${kozos-on-zero-riscy}\src\main\kozos\bootload
"c:\Program Files (x86)\GnuWin32\bin\make.exe"
cd ${kozos-on-zero-riscy}\src\main\kozos\os
"c:\Program Files (x86)\GnuWin32\bin\make.exe"
```

## zero-riscy シミュレータの実行

```
cd ${kozos-on-zero-riscy}
copy src\main\kozos\bootload\kzload.ihex loadmem.ihex
copy src\main\kozos\os\kozos xmodem.dat
sim\Vzeroriscy_verilator_top
```

実行結果  
下の ```<- type``` のコマンドを入力

```
Running ...
kzload (kozos boot loader) started.
kzload> load <- type
XMODEM receive succeeded.
kzload> run <- type
starting from entry point: 80080000
Hello World!
> echo aaa <- type
 aaa
> q
```

## シミュレーションログの解析
### 命令トレースの見方
まだ

### kozos の逆アセンブル
まだ

### 発展：VCD 波形取得
sim 実行時に ``` --vcdfile=board.vcd``` を指定する。

```
sim\Vzeroriscy_verilator_top --vcdfile=board.vcd
```

取得時間の指定もできます。
- 開始時刻 ```--vcdstart=${TIME}```
- 終了時刻 ```--vcdend=${TIME}```

${TIME} の目安はシミュレーション実行ログの ```Cycles×100+1000``` くらい

## リンク
[zero-riscy シミュレータのソース](https://github.com/tom01h/zero-riscy-test)  
[zero-riscy コアのソース](https://github.com/tom01h/zero-riscy) (このリポジトリで使っているもの)  
[zero-riscy コアのソース](https://github.com/pulp-platform/zero-riscy) (オリジナル)  
[RISC-V ソフト開発環境のソース](https://github.com/riscv/riscv-gnu-toolchain)  
[RISC-V の命令セット仕様](https://riscv.org/specifications/)

## ライセンス
改変元のライセンス条件です。
#### kozos
kozos ディレクトリを参照ください。  
#### zero-riscy
以下と ```LICENSE.zero-riscy``` を参照ください。  

```
// Copyright 2017 ETH Zurich and University of Bologna.
// Copyright and related rights are licensed under the Solderpad Hardware
// License, Version 0.51 (the “License”); you may not use this file except in
// compliance with the License.  You may obtain a copy of the License at
// http://solderpad.org/licenses/SHL-0.51. Unless required by applicable law
// or agreed to in writing, software, hardware and materials distributed under
// this License is distributed on an “AS IS” BASIS, WITHOUT WARRANTIES OR
// CONDITIONS OF ANY KIND, either express or implied. See the License for the
// specific language governing permissions and limitations under the License.
```

#### シミュレーション環境
V-scale のシミュレーション環境をもとに作成したため、V-scale のライセンス条件を受けます(多分…)。  
V-scale のライセンスは ```LICENSE.V-scale``` を参照ください。  
