on: [push, pull_request]
name: Test
jobs:
  test:
    strategy:
      matrix:
        go-version: [1.14.x, 1.15.x]
        os: [ubuntu-latest, macos-latest]
    runs-on: ${{ matrix.os }}
    steps:
      - name: Install Go
        uses: actions/setup-go@v2
        with:
          go-version: ${{ matrix.go-version }}
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Test
        run: go test -mod=vendor ./...
