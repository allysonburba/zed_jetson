build:
	@cp /etc/nv_tegra_release .nv_tegra_release
	docker build -t personalroboticsimperial/prl:jetson2004-cuda122-noetic-zed40 .
	@rm -Rf .nv_tegra_release

run:
	@docker container stop jetson20noetic-zed40 || true && docker container rm jetson20noetic-zed40 || true
	docker run \
		-it \
		-e "DISPLAY" \
		-e "QT_X11_NO_MITSHM=1" \
		-e "XAUTHORITY=${XAUTH}" \
		-e ROS_MASTER_URI \
		-e ROS_IP \
		-v ~/.Xauthority:/root/.Xauthority:rw \
		-v "/tmp/.X11-unix:/tmp/.X11-unix:rw" \
		--network host \
		--privileged \
		--name jetson20noetic-zed40 \
		--runtime=nvidia \
		personalroboticsimperial/prl:jetson2004-cuda122-noetic-zed40

push:
	docker push personalroboticsimperial/prl:jetson2004-cuda122-noetic-zed40