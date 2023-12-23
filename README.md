  publish:
    runs-on: ubuntu-latest
    needs: [package]
    steps: 
        - uses: actions/checkout@v3
        - uses: actions/download-artifact@v3
            with:
            name: api-jar
            path: target
        -   uses: docker/login-action@v2
            with:
                username: ${{ secrets.DOCKERHUB_USERNAME }}
                password: ${{ secrets.DOCKERHUB_PASSWORD }}
        - name: Build and push
            uses: docker/build-push-action@v4
            with:
            context: .
            push: true
            tags: srghouse/tempjavaapi:1.1

    