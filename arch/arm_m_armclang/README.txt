                       ARM-M依存部(ARMCLANG版) 

                                   Last Modified:2018 Apr 20 13:26:36

本ディレクトリ（./arch/arm_m_armclang）は，armv7mアーキテクチャのコア
及び，armv7mアーキテクチャのコアを用いたチップに依存し，コンパイラとし
てARMCLANGを対象した記述を置くためのディレクトリである．

GCC版と共有するファイルはARM依存部(GCC版) ディレクトリ，ARM依存部
(ARMCC版) ディレクトリのいずれかに配置する．

common以下のファイルで共有するファイルはARM依存部(GCC版)に配置している．

その他のルールはGCC版と同様である．


○ARMCLANG対応について

ARMCLANGはGNUコンパイラとほぼ互換であるため，ソースコードの多くは，GNU
版を使用する．

アセンブラに関しては，ARMASMはGNUのASとシンタックスが異なるが，
ARMCLANGから呼び出されるアセンブラはGNUのASと互換性があるため，こちら
を使用する．

リンカに関しては，ARMLINKを使用する必要があり，GNU版と互換性がない．そ
のため，各Makefileに関してはGNU版と異なるものを用意する必要がある．

以上により，ARMCLANG独自のファイルとして次のものを用意している．

./common
  ./core_asm.inc    : セクション情報がGNUと互換性がないため
  ./core_cfg1_out.h : リンク時の警告を回避するための定義が必要なため
  ./core_weak.S     : リンカスクリプトでのweak定義がないため，
                      software_init_hook 等のweak関数を定義．  
                        
../armclang
  ./Makefile.sample  : ARMCLANG用のMakefile
  ./tool_stddef.h    : GNU版と同等だが今後変更する可能性があるため用意．

以上．
