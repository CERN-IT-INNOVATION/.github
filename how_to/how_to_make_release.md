# Package Release Tutorial

## Make a new release on GitHub

To create a new code release on GitHub, follow this
[doc](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository).

## Publish on Zenodo references

- Publish code on Zenodo to obtain DOI and citation details.  
  Follow the GitHub
  [Referencing and citing content](https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content)
  tutorial.

  **Note:**  
    if the repository is owned by an organization, the organization owner
    may need to [approve access](https://docs.github.com/en/organizations/restricting-access-to-your-organizations-data/approving-oauth-apps-for-your-organization) for Zenodo application

## Before release referencing

> - Before making a new release on Zenodo, initiate a new version uploading and
>    reserve a DOI.
> - Edit all the citation information in the docs and READMEs
> - Complete the Zenodo release, making a new release on GitHub

It is important to know citations and reference of the published material before
making the release. Otherwise all the docs and READMEs will contain outdated
references.

### Zenodo badge

Do not link the badge given by zenodo when creating a new release, but link
the latest badge of the repository itself as described
[here](https://gist.github.com/seignovert/ae6771f400ca464d294261f42900823a).  
Must get the relevant GitHub repository id from the `api` website at
`https://api.github.com/repos/{user}/{repo}`, with the correct `user` and
`repo` fields.
  
  **Note:**  
  If the repo is owned by an organization, replace the `user` field with the
  organization name.

### Citing the software

Generate the `CITATION.cff` file (this is for software, use a badge or text in
the README.md for articles instead.)  
More information [here](https://citation-file-format.github.io/), and use the
template provided by the useful
[cffinit website](https://citation-file-format.github.io/cff-initializer-javascript/).

  **Note:**  
  use `given-names` and `family-names` for author name, otherwise it will
  not be rendered correctly in the BibTex style. Do not use `name-particle`.
