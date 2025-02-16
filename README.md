# Obico-HA
Addon for Home Assistant to run an [Obico](https://www.obico.io/) backend [server](https://github.com/TheSpaghettiDetective/obico-server).

Based on [ha-bambu-lab-p1-spaghetti-detection](https://github.com/nberktumer/ha-bambu-lab-p1-spaghetti-detection/) by [nberktumer](https://github.com/nberktumer).

## API Endpoints
### `/p/`
- Example request: `GET http://localhost:3333/p/?img=https://www.example.com/image.jpg`
- Example response:
	```json
	{
		"detections": [
			[
				0.541085422039032,
				[
					422.7984619140625,
					236.30227661132812,
					61.9364013671875,
					74.49552917480469
				]
			],
			[
				0.43781569600105286,
				[
					426.05596923828125,
					264.619140625,
					42.386478424072266,
					4.73854064941406
				]
			],
			[
				0.2545202076435089,
				[
					423.3209533691406,
					238.6829071044922,
					113.47953796386719,
					135.73854064941406
				]
			],
			[
				0.20370429754257202,
				[
					456.3966369628906,
					236.23785400390625,
					39.029632568359375,
					67.34481811523438
				]
			]
		]
	}
	```

## `/hc/`
- Example request: `GET http://localhost:3333/hc/`
- Example response: `ok` (returns `ok` if the server is running and the model is loaded)

## `/detect/`
- Similar to `/p/` except it also includes a base64 image string in the response showing the detections. Inspired from the [Obico ML HA Addon](https://github.com/nobodyguy/obico_ml_ha_addon) by [nobodyguy](https://github.com/nobodyguy)
- Example request body (must be a `POST` request):
	```json
	{
		"img": "base64_encoded_image_as_string",
		"threshold": 0.08,
		"rectangleColor": [0, 0, 255],
		"rectangleThickness": 5,
		"fontFace": "FONT_HERSHEY_SIMPLEX",
		"fontScale": 1.5,
		"textColor": [0, 0, 255],
		"textThickness": 2
	}
	```
- Example response:
	```json
	{
		"image_with_detections": "base64_encoded_image_as_string",
		"detections": [
			[
				0.541085422039032,
				[
					422.7984619140625,
					236.30227661132812,
					61.9364013671875,
					74.49552917480469
				]
			],
			[
				0.43781569600105286,
				[
					426.05596923828125,
					264.619140625,
					42.386478424072266,
					4.73854064941406
				]
			],
			[
				0.2545202076435089,
				[
					423.3209533691406,
					238.6829071044922,
					113.47953796386719,
					135.73854064941406
				]
			],
			[
				0.20370429754257202,
				[
					456.3966369628906,
					236.23785400390625,
					39.029632568359375,
					67.34481811523438
				]
			]
		]
	}
	```

## `/check/`
- Similar to `/p/` except it takes a Home Assistant camera entity name rather than a URL of the image
- Example request: `GET http://localhost:3333/check/?entity_id=camera.example_camera`
- Headers: {}
- Rxample response: 
	```json
	{
		"detections": [
			[
				0.541085422039032,
				[
					422.7984619140625,
					236.30227661132812,
					61.9364013671875,
					74.49552917480469
				]
			],
			[
				0.43781569600105286,
				[
					426.05596923828125,
					264.619140625,
					42.386478424072266,
					4.73854064941406
				]
			],
			[
				0.2545202076435089,
				[
					423.3209533691406,
					238.6829071044922,
					113.47953796386719,
					135.73854064941406
				]
			],
			[
				0.20370429754257202,
				[
					456.3966369628906,
					236.23785400390625,
					39.029632568359375,
					67.34481811523438
				]
			]
		]
	}
	```