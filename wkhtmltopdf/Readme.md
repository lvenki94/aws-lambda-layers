# Build Command

docker run --rm \
  -v "$(pwd)/output":/output \
  -v "$(pwd)/fonts":/build/fonts \
  -v "$(pwd)/build_lambda_layer.sh":/build/build_lambda_layer.sh \
  -w /build \
  --platform linux/amd64 \
  amazonlinux:latest \
  bash /build/build_lambda_layer.sh