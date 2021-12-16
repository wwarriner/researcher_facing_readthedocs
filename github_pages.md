# GitHub Pages

## One-time setup

1. Rename repository to `uabrc.github.io` to match pattern requirements.
2. Modify `.gitignore`, commit, push.

   1. Add lines

        ```{shell}
        !/build/html
        /build/html/*
        !build/html/.nojekyll
        /docs
        ```

3. Modify `make.bat` and `Makefile`, commit, push.

   1. `make.bat`

      1. After the line starting with `%SPHINXBUILD -M %1` add

            ```{batch}
            if "%1" == "html" (
                copy NUL "%BUILDDIR%/html/.nojekyll"
                rmdir /s/q "docs\" > NUL 2> NUL
                mkdir "docs\" > NUL 2> NUL
                move /y "%BUILDDIR%/html" "docs\"
            )
            ```

      2. `.nojekyll` is needed to use CSS correctly
      3. The rest is for putting the build output in a directory GitHub Pages knows about

   2. `Makefile`

      1. As `make.bat` but in `make` style.

4. Create branch `gh-pages`.

   1. Switch to `gh-pages` branch.
   2. Comment out `/docs` in `.gitignore`, commit, push.
   3. Build with `make.bat` or `make`, commit, push.

5. Prepare Pages settings.
   1. Go to <https://github.com/uabrc/uabrc.github.io>.
   2. Click "Settings" in the tabs beneath the repo name.
   3. Click "Pages" in the left-hand menu.
   4. Under "Source" click the first drop-down and select `gh-pages`.
   5. Click the second drop-down and select `/docs`.
   6. Click the "Save" button.

6. Verify by visiting https://uabrc.github.io.

## Workflow

1. Make changes to `main` via Pull Request from forks.
2. Merge changes into `gh-pages` when satisfied.
3. Build from `gh-pages` branch.
4. Verify by visiting <https://uabrc.github.io>.
