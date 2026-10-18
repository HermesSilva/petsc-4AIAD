# PETSc for Tootega AIAD (Windows)

This is a fork of **[PETSc](https://gitlab.com/petsc/petsc)** (through its GitHub mirror
[petsc/petsc](https://github.com/petsc/petsc)), maintained for **Tootega AIAD** (Artificial
Intelligence-Aided Design), a Windows-only CAD/CAE tool built on OpenUSD, DirectX 12 and CUDA.

> The original README is kept unchanged in **[README.upstream.md](README.upstream.md)**.
> Everything about PETSc itself is documented there and at [petsc.org](https://petsc.org).

## Why this fork exists

PETSc is required by [honee-4AIAD](https://github.com/HermesSilva/honee-4AIAD) (compressible
Navier-Stokes) and, through SLEPc, is one of the eigenvalue-solver options of
[palace-4AIAD](https://github.com/HermesSilva/palace-4AIAD). AIAD runs **only on Windows**. PETSc
does document Windows builds with MSVC, but its `configure` relies on a POSIX shell, and the
combination MSVC + MS-MPI + CUDA + libCEED that AIAD needs is not a common configuration. This
fork keeps that configuration building and working.

## What changes (and why)

| Change | Why |
|--------|-----|
| A reproducible **Windows configuration** (`arch-windows-msvc-cuda`): MSVC v145, MS-MPI, CUDA, Intel MKL | the exact toolchain used by the rest of AIAD |
| `configure` run from the Git for Windows (MSYS2) shell, **only at build time** | PETSc's configure needs a POSIX shell; the product itself stays native Windows |
| **libCEED** from [libceed-4AIAD](https://github.com/HermesSilva/libceed-4AIAD) | the one libCEED shared by MFEM, Palace and HONEE |
| Fixes for MSVC/nvcc issues found along the way, kept small and isolated | so they are easy to rebase and, when possible, to send upstream |
| PETSc built **without CUDA** as an intermediate step, if needed | to unblock HONEE before the GPU path is complete |

## Status

**No source changes yet.** At this point the only differences from upstream are this README and
the original README renamed to `README.upstream.md`. The Windows work is planned in the AIAD
roadmap (spike S7, milestone F9).

## Branches

| Branch | Content |
|--------|---------|
| `main` | mirror of PETSc `main`, never modified |
| `main-4AIAD` (default) | `main` + the Windows changes, rebased periodically onto upstream |

## License

Same as upstream: **BSD 2-Clause** (see [LICENSE](LICENSE)). Changes made in this fork are
released under the same license.
