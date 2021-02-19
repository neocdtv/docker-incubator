# Run spotify in a container
#
# docker run -d \
#	-v /etc/localtime:/etc/localtime:ro \
#	-v /tmp/.X11-unix:/tmp/.X11-unix \
#	-e DISPLAY=unix$DISPLAY \
#	--device /dev/snd:/dev/snd \
#	-v $HOME/.spotify/config:/home/spotify/.config/spotify \
#	-v $HOME/.spotify/cache:/home/spotify/spotify \
#	--name spotify \
#	jess/spotify
#
FROM debian:sid-slim

RUN	apt-get update && apt-get install -y \
	dirmngr \
	gnupg \
	--no-install-recommends \
	&& apt-get update && apt-get install -y \
	alsa-utils \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	libpulse0 \
	xdg-utils \
	chromium \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV HOME /home/spotify
RUN useradd --create-home --home-dir $HOME spotify \
	&& gpasswd -a spotify audio \
	&& chown -R spotify:spotify $HOME

WORKDIR $HOME
USER spotify

# make search bar text better
RUN echo "QLineEdit { color: #000 }" > /home/spotify/spotify-override.css

ENTRYPOINT [ "chromium" ]