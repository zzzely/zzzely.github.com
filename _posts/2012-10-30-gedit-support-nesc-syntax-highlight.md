---
layout: post
title: gedit支持nesC语法高亮
comments: true
categories: Coding
tags: [nesc, gedit, tinyos, syntax, highlight]
---
{% include JB/setup %}

在虚拟机的Ubuntu环境下，如果不太习惯Vim这种带有模式的编辑器，可以选择默认的gedit来编写nesC程序，它也可以添加对nesC语法高亮的支持。

将下面xml内容保存为nesc.lang
然后

`sudo cp nesc.lang /usr/share/gtksourceview-2.0/language-specs/`

重启gedit就可以了。

<ol class="linenums">
	<li class="L0"><span class="pun">&lt;?</span><span class="pln">xml version</span><span class="pun">=</span><span class="str">"1.0"</span><span class="pln"> encoding</span><span class="pun">=</span><span class="str">"UTF-8"</span><span class="pun">?&gt;</span></li>
	<li class="L1"><span class="com">&lt;!--</span></li>
	<li class="L2"><span class="com"> Authors: Ariel Núñez, Marco Barisione, Emanuele Aina</span></li>
	<li class="L3"><span class="com"> Copyright (C) 2005-2007 Marco Barisione &lt;barisione@gmail.com&gt;</span></li>
	<li class="L4"><span class="com"> Copyright (C) 2005-2007 Emanuele Aina</span></li>
	<li class="L5"><span class="com"> Copyright (C) 2007 Ariel Núñez (Adapted to NesC the cpp.lang written by Marco and Emanuele)</span></li>
	<li class="L6"><span class="com"> </span></li>
	<li class="L7"><span class="com"> This library is free software; you can redistribute it and/or</span></li>
	<li class="L8"><span class="com"> modify it under the terms of the GNU Library General Public</span></li>
	<li class="L9"><span class="com"> License as published by the Free Software Foundation; either</span></li>
	<li class="L0"><span class="com"> version 2 of the License, or (at your option) any later version.</span></li>
	<li class="L1"><span class="com"> </span></li>
	<li class="L2"><span class="com"> This library is distributed in the hope that it will be useful,</span></li>
	<li class="L3"><span class="com"> but WITHOUT ANY WARRANTY; without even the implied warranty of</span></li>
	<li class="L4"><span class="com"> MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU</span></li>
	<li class="L5"><span class="com"> Library General Public License for more details.</span></li>
	<li class="L6"><span class="com"> </span></li>
	<li class="L7"><span class="com"> You should have received a copy of the GNU Library General Public</span></li>
	<li class="L8"><span class="com"> License along with this library; if not, write to the</span></li>
	<li class="L9"><span class="com"> Free Software Foundation, Inc., 59 Temple Place - Suite 330,</span></li>
	<li class="L0"><span class="com"> Boston, MA 02111-1307, USA.</span></li>
	<li class="L1"><span class="com"> </span></li>
	<li class="L2"><span class="com">--&gt;</span></li>
	<li class="L3"><span class="tag">&lt;language</span><span class="pln"> </span><span class="atn">id</span><span class="pun">=</span><span class="atv">"nc"</span><span class="pln"> _</span><span class="atn">name</span><span class="pun">=</span><span class="atv">"NesC"</span><span class="pln"> </span><span class="atn">version</span><span class="pun">=</span><span class="atv">"2.0"</span><span class="pln"> _</span><span class="atn">section</span><span class="pun">=</span><span class="atv">"Sources"</span><span class="tag">&gt;</span></li>
	<li class="L4"><span class="pln">    </span><span class="tag">&lt;metadata&gt;</span></li>
	<li class="L5"><span class="pln">      </span><span class="tag">&lt;property</span><span class="pln"> </span><span class="atn">name</span><span class="pun">=</span><span class="atv">"mimetypes"</span><span class="tag">&gt;</span><span class="pln">application/x-netcdf;text/x-chdr;text/x-csrc;text/plain</span><span class="tag">&lt;/property&gt;</span></li>
	<li class="L6"><span class="pln">      </span><span class="tag">&lt;property</span><span class="pln"> </span><span class="atn">name</span><span class="pun">=</span><span class="atv">"globs"</span><span class="tag">&gt;</span><span class="pln">*.nc</span><span class="tag">&lt;/property&gt;</span></li>
	<li class="L7"><span class="pln">      </span><span class="tag">&lt;property</span><span class="pln"> </span><span class="atn">name</span><span class="pun">=</span><span class="atv">"line-comment-start"</span><span class="tag">&gt;</span><span class="pln">//</span><span class="tag">&lt;/property&gt;</span></li>
	<li class="L8"><span class="pln">      </span><span class="tag">&lt;property</span><span class="pln"> </span><span class="atn">name</span><span class="pun">=</span><span class="atv">"block-comment-start"</span><span class="tag">&gt;</span><span class="pln">/*</span><span class="tag">&lt;/property&gt;</span></li>
	<li class="L9"><span class="pln">      </span><span class="tag">&lt;property</span><span class="pln"> </span><span class="atn">name</span><span class="pun">=</span><span class="atv">"block-comment-end"</span><span class="tag">&gt;</span><span class="pln">*/</span><span class="tag">&lt;/property&gt;</span></li>
	<li class="L0"><span class="pln">    </span><span class="tag">&lt;/metadata&gt;</span></li>
	<li class="L1"><span class="pln"> </span></li>
	<li class="L2"><span class="pln">    </span><span class="tag">&lt;styles&gt;</span></li>
	<li class="L3"><span class="pln">        </span><span class="tag">&lt;style</span><span class="pln"> </span><span class="atn">id</span><span class="pun">=</span><span class="atv">"keyword"</span><span class="pln"> _</span><span class="atn">name</span><span class="pun">=</span><span class="atv">"Keyword"</span><span class="pln"> </span><span class="atn">map-to</span><span class="pun">=</span><span class="atv">"c:keyword"</span><span class="tag">/&gt;</span></li>
	<li class="L4"><span class="pln">        </span><span class="tag">&lt;style</span><span class="pln"> </span><span class="atn">id</span><span class="pun">=</span><span class="atv">"type"</span><span class="pln"> _</span><span class="atn">name</span><span class="pun">=</span><span class="atv">"Data Type"</span><span class="pln"> </span><span class="atn">map-to</span><span class="pun">=</span><span class="atv">"c:type"</span><span class="tag">/&gt;</span></li>
	<li class="L5"><span class="pln">        </span><span class="tag">&lt;style</span><span class="pln"> </span><span class="atn">id</span><span class="pun">=</span><span class="atv">"common-defines"</span><span class="pln"> _</span><span class="atn">name</span><span class="pun">=</span><span class="atv">"Common Defines"</span><span class="pln"> </span><span class="atn">map-to</span><span class="pun">=</span><span class="atv">"c:common-defines"</span><span class="tag">/&gt;</span></li>
	<li class="L6"><span class="pln">    </span><span class="tag">&lt;/styles&gt;</span></li>
	<li class="L7"><span class="pln"> </span></li>
	<li class="L8"><span class="pln">    </span><span class="tag">&lt;definitions&gt;</span></li>
	<li class="L9"><span class="pln">        </span><span class="com">&lt;!-- NesC-specific stuff (i.e. stuff which is not C) --&gt;</span></li>
	<li class="L0"><span class="pln">        </span><span class="tag">&lt;context</span><span class="pln"> </span><span class="atn">id</span><span class="pun">=</span><span class="atv">"ncc-proper"</span><span class="tag">&gt;</span></li>
	<li class="L1"><span class="pln">            </span><span class="tag">&lt;include&gt;</span></li>
	<li class="L2"><span class="pln">                </span><span class="tag">&lt;context</span><span class="pln"> </span><span class="atn">id</span><span class="pun">=</span><span class="atv">"keywords"</span><span class="pln"> </span><span class="atn">style-ref</span><span class="pun">=</span><span class="atv">"keyword"</span><span class="tag">&gt;</span></li>
	<li class="L3"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">async</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L4"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">generic</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L5"><span class="pln">              </span><span class="tag">&lt;keyword&gt;</span><span class="pln">interface</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L6"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">norace</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L7"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">command</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L8"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">module</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L9"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">post</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L0"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">provides</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L1"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">components</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L2"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">implementation</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L3"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">configuration</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L4"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">includes</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L5"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">uses</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L6"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">call</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L7"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">dbg</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L8"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">event</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L9"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">task</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L0"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">signal</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L1"><span class="pln">                </span><span class="tag">&lt;/context&gt;</span></li>
	<li class="L2"><span class="pln"> </span></li>
	<li class="L3"><span class="pln">                </span><span class="tag">&lt;context</span><span class="pln"> </span><span class="atn">id</span><span class="pun">=</span><span class="atv">"types"</span><span class="pln"> </span><span class="atn">style-ref</span><span class="pun">=</span><span class="atv">"type"</span><span class="tag">&gt;</span></li>
	<li class="L4"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">uint8_t</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L5"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">uint16_t</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L6"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">uint32_t</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L7"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">bool</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L8"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">result_t</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L9"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">int32_t</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L0"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">int16_t</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L1"><span class="pln">            </span><span class="tag">&lt;keyword&gt;</span><span class="pln">int8_t</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L2"><span class="pln">                </span><span class="tag">&lt;/context&gt;</span></li>
	<li class="L3"><span class="pln"> </span></li>
	<li class="L4"><span class="pln">                </span><span class="tag">&lt;context</span><span class="pln"> </span><span class="atn">id</span><span class="pun">=</span><span class="atv">"common-defines"</span><span class="pln"> </span><span class="atn">style-ref</span><span class="pun">=</span><span class="atv">"common-defines"</span><span class="tag">&gt;</span></li>
	<li class="L5"><span class="pln">                    </span><span class="tag">&lt;keyword&gt;</span><span class="pln">__STDC__</span><span class="tag">&lt;/keyword&gt;</span></li>
	<li class="L6"><span class="pln">                </span><span class="tag">&lt;/context&gt;</span></li>
	<li class="L7"><span class="pln">            </span><span class="tag">&lt;/include&gt;</span></li>
	<li class="L8"><span class="pln">        </span><span class="tag">&lt;/context&gt;</span></li>
	<li class="L9"><span class="pln"> </span></li>
	<li class="L0"><span class="pln">        </span><span class="com">&lt;!-- actual language definition: NesC-specific stuff plus everything from C --&gt;</span></li>
	<li class="L1"><span class="pln">        </span><span class="tag">&lt;context</span><span class="pln"> </span><span class="atn">id</span><span class="pun">=</span><span class="atv">"nc"</span><span class="tag">&gt;</span></li>
	<li class="L2"><span class="pln">            </span><span class="tag">&lt;include&gt;</span></li>
	<li class="L3"><span class="pln">                </span><span class="tag">&lt;context</span><span class="pln"> </span><span class="atn">ref</span><span class="pun">=</span><span class="atv">"ncc-proper"</span><span class="tag">/&gt;</span></li>
	<li class="L4"><span class="pln">                </span><span class="tag">&lt;context</span><span class="pln"> </span><span class="atn">ref</span><span class="pun">=</span><span class="atv">"c:c"</span><span class="tag">/&gt;</span></li>
	<li class="L5"><span class="pln">            </span><span class="tag">&lt;/include&gt;</span></li>
	<li class="L6"><span class="pln">        </span><span class="tag">&lt;/context&gt;</span></li>
	<li class="L7"><span class="pln">    </span><span class="tag">&lt;/definitions&gt;</span></li>
	<li class="L8"><span class="tag">&lt;/language&gt;</span></li>
</ol>
