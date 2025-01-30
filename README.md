The Survival Probability Adapted Nuclear Norm Shrinkage (SPANNS) Denoiser
=========================================================================

A simple denoiser compatible with VapourSynth.

Supported Formats
-----------------
The denoiser core supports any 2D numeric matrices. For VapourSynth usage, you need to provide clips with full precision and planes of the same dimensions (e.g., convert YUV422 to YUV444PS or RGBS first).

Usage
-----

`spanns.spanns(clip, ...)`

### Arguments:
- **clip** (*vs.VideoNode*): The original video node.
- **sigma** (*int*): Denoising strength. Default is `1`.
- **tol** (*float*): Noise tolerance in the range [0, 1]. Default is `0.7`.
- **cutoff** (*float*): high information components cutoff point. either provide `cutoff < 1.` as a percentile cutoff, or `cutoff >= 1` as a fix integer (rounded) number of components to cutoff. Default is `0.9`.
- **ref** (*vs.VideoNode*): Reference clip, a blurred one obtained from the original. It serves as an alternative way to control denoising strength. If provided, `sigma` will be ignored. Default is a box blur with radius equal to `sigma`.
- **planes** (*Sequence[int]*): Indices of planes to process. Default is `[0, 1, 2]`.

### Returns:
The denoised clip (*vs.VideoNode*).

TODO
----
- IDK Yet

Background
----------
In 2019, the author was disappointed by the practical performance of WNNM, a well-regarded but ~~f*cking~~ cumbersome denoising approach proposed years earlier. One should notice that the fundamental assumption of NNM, $\lVert M\rVert_{nuc} < \lVert N\rVert_{nuc} \implies \text{M embeds less noise}$ is a false statement either visually or in the sense of compression ratio. Although there have been improvements to the technique, most rely on patch matching and increasing complexity, which the author finds unappealing. Reflecting on its limitations, the author implemented a better ~~but still sh\*t~~ heuristic method: SPANNS.

In essence, SPANNS damps the orthogonal components according to the noise's survival probability along the axis of component magnitude (the singular values). While the denoising results might not stand out in today's advanced landscape, the author hopes someone can appreciate its simplicity.

Buy Me Coffee
-------------
Don't, I can't have coffee.
