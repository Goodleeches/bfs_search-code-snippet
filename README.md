# bfs_search-code-snippet

	// bfs search
	int startX = getArrIndex().x;
	int startY = getArrIndex().y;

	queue<pair<pair<int, int>, int>> q;
	q.push(make_pair(make_pair(startX, startY), 0));

	while (!q.empty())
	{
		int x = q.front().first.first;
		int y = q.front().first.second;
		int dist = q.front().second;

		q.pop();

		for (size_t i = 0; i < 8; i++)
		{
			int nx = x + dx[i];
			int ny = y + dy[i];

			if (0 <= nx && nx < MAP_WIDTH && 0 <= ny && ny < MAP_HEIGHT)
			{
				if (tmpcheckMap[ny][nx])
					continue;

				tmpcheckMap[ny][nx] = true;
				distMap[ny][nx] = dist + 1;
				q.push(make_pair(make_pair(nx, ny), dist + 1));
			}
		}
	}

	int iMin = 100;
	int retX = -1;
	int retY = -1;
	for (size_t y = 0; y < MAP_HEIGHT; y++)
	{
		for (size_t x = 0; x < MAP_WIDTH; x++)
		{
			if (!checkMap[y][x])
			{
				if (iMin > distMap[y][x])
				{
					iMin = distMap[y][x];
					retX = x;
					retY = y;
				}
			}
		}
	}

	if (retX == -1 && retY == -1)
	{
		// error
		return;
	}
