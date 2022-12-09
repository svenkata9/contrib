# Enclave signing with a HSM using OpenSSL engine

SGX enclaves must be signed using a 3072-bit RSA key. This key needs to be
protected and must not be disclosed to anyone. Typically for production
deployments, you should use a key secured in a Hardware Security Module (HSM).

This directory contains the plugin to Gramine tools and templates that enable
support for production signing of SGX enclaves using keys from a HSM accessible
using OpenSSL engine.

## Prerequisites for SGX enclave signing

- OpenSSL engine-based access available for the HSM.
- 3072-bit RSA private key with a public exponent 3 created in this HSM. Please
  note that only Managed HSM supports setting public exponent.
- Tools installed and the user is authenticated to access to the HSM.

## Running

The command to sign the enclave with a HSM using OpenSSL engine looks like this:
```
./gramine-sgx-ossl-sign \
  --manifest <your-app-manifest> --output <your-app-manifest>.sgx \
  --engine openssl_engine --key sgx_sign_key
```

where `sgx_sign_key` is the name of the RSA private key created in the HSM
accessible through the engine `openssl_engine`.

## Templates for use with Gramine Shielded Containers (GSC)

GSC `sign-image` command can take in a user supplied Dockerfile
as an argument to `--template` and sign the graminized docker image. These
templates can be used when a HSM is needed for signing. This directory has
templates for using OpenSSL engine to sign the graminized docker image. Please
note that these are templates and the users will need to update the template
with the required details to make it a 'self-contained' Dockerfile before
passing it to `sign-image` command.


