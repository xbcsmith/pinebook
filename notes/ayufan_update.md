# Update Ayufan Release

## Script

    VERSION="$2"

    if [[ -z "$VERSION" ]]; then
        VERSION=$(curl -f -sS https://api.github.com/repos/$REPO/releases/latest | jq -r ".tag_name")
        if [ -z "$VERSION" ]; then
            echo "Latest release was not for $1."
            echo "Please go to: https://github.com/$REPO/releases/latest"
            exit 1
        fi

        echo "Using latest release: $VERSION from https://github.com/$REPO/releases."
    fi

	sudo /usr/local/sbin/pine64_update_kernel.sh $VERSION
	sudo /usr/local/sbin/pine64_update_uboot.sh $VERSION
	sudo /usr/local/sbin/pine64_update_package.sh $VERSION

