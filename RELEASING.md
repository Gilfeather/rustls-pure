# Releasing rustls-pure

rustls-pure is released only when it changes (a fix, a new minimum Rust or rustls version, a
README that crates.io should show):

1. In a pull request: raise `version` in `Cargo.toml` (before 1.0, a patch for fixes and docs,
   a minor for anything breaking, a higher MSRV or a new rustls minor version), and move the
   entries in `CHANGELOG.md` under that version with the date.
2. Merge, then tag that `main` commit and push the tag:
   `git tag v0.15.5 && git push origin v0.15.5`.
3. `.github/workflows/release.yml` checks that the tag matches the version, runs the tests and
   publishes it through crates.io Trusted Publishing. A version already on crates.io is not
   published again.
4. Dependents that need the new version raise their requirement; Furnace's furnace-server
   depends on it from crates.io.

A vulnerability fix follows [SECURITY.md](SECURITY.md).

Releases up to 0.15.4 were made from the [Furnace](https://github.com/Gilfeather/furnace)
repository, tagged `rustls-pure-v<version>` there; from this repository the tags are
`v<version>`.

## Trusted Publishing

On crates.io, rustls-pure → Settings → Trusted Publishing → Add → GitHub, with repository owner
`Gilfeather`, repository name `rustls-pure`, workflow filename `release.yml` and no environment.
The entries for the Furnace repository can be removed once this one is in place.
