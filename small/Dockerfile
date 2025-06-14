FROM oscarlevin/pretext:lite

# Set TMPDIR to avoid permission issues on ARM architectures
ENV TMPDIR=/

RUN wget -O TinyTex.sh "https://yihui.org/tinytex/install-bin-unix.sh" \
&& bash TinyTex.sh \
&& rm TinyTex.sh

#TinyTeX installs links to the executable in /root/bin, so we need to add that to the PATH
ENV PATH="/root/bin:$PATH"

SHELL ["/bin/bash", "-i", "-c"]

RUN tlmgr install adjustbox amscdx bold-extra braket bussproofs cancel carlisle cases chessfss circuitikz colortbl enumitem extpfeil fontawesome5 fontaxes gensymb imakeidx jknapltx kastrup lambda-lists listings listingsutf8 makeindex marvosym mathalpha mathtools menukeys mhchem microtype musicography newpx newtx nicematrix pdfcol pdfpages pdflscape pgfplots phaistos physics polyglossia pstricks realscripts relsize siunitx skak skaknew smartdiagram snapshot stmaryrd tcolorbox tikz-cd tikzfill titlesec txfonts ulem upquote was xfrac xltxtra xpatch xstring \
&& tlmgr path add

#  Ensure fonts provided by TinyTeX are available, as suggested in the pretext guide

RUN fontconfig_path="/etc/fonts/conf.d/09-texlive-fonts.conf" && \
    fontconfig="<?xml version=\"1.0\"?>\n<!DOCTYPE fontconfig SYSTEM \"fonts.dtd\">\n<fontconfig>\n  <dir>~/.TinyTeX/texmf-dist/fonts</dir>\n  <dir>~/.TinyTeX/texmf-local/fonts</dir>\n</fontconfig>" && \
    if [ ! -f "$fontconfig_path" ]; then \
        echo "Creating fontconfig file at $fontconfig_path"; \
        echo -e "$fontconfig" > "$fontconfig_path"; \
    else \
        echo "Fontconfig file already exists at $fontconfig_path"; \
    fi && \
    fc-cache -f -v

